---
title: 分面点图优化
date: 2023-06-02 15:46:30
categories: 
- 图片美化
tags: ['技术']
hide: true
---
按group对dotplot进行分面拆分。

<!-- more -->
当Seurat::DotPlot同时使用group.by和split.by时，列的名称将会由split.by进行设置，行名（data.plot$id）将会是group.by和split.by的组合（通过下划线连接）。

![](Error.png)

这种方式获得的图片并不太美观，且在group.by和split.by分组数量较多时会导致报错。因此对其进行优化，美化代码如下：

~~~R
library(Seurat)
library(ggplot2)
library(ggpubr)

#选取细胞类型非Pre-B_cell_CD34-的细胞，保证在两组中一致
`%!in%` <- Negate(`%in%`)
seurat_ob = subset(seurat_ob, celltype %!in% c("Pre-B_cell_CD34-"))

#按group拆分seurat对象
split <- SplitObject(seurat_ob,split.by="orig.ident")
order=sort(unique(seurat_ob@meta.data[,"orig.ident"]))

#横坐标为Celltype
ggfeature = lapply( order, function(x)
dot_plot = DotPlot(object =split[[ x ]], features = c("EPCAM","CD19","KRT8","CD3E"), group.by = "celltype") + guides(color = guide_colorbar(order = 1, title = "Average Expression"))+ coord_flip()+ theme(axis.text.x = element_text(angle = 90),axis.title.x = element_blank(),axis.title.y = element_blank()) +labs(title=x )+ scale_colour_gradientn(colors= c("grey","#9E0142")))

#直接用ggpubr拼图
plot <- do.call(ggpubr::ggarrange, c(ggfeature, list(ncol = 2,
                            nrow =1,
                            common.legend = TRUE,
                            legend = "right",
                            align = "none")))

ggsave("Dotplot.pdf",plot)
~~~
