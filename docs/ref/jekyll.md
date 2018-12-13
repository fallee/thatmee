---
title: jekyll 参考样例
---

## values

### site

|name|value|
|:---:|---|
|time|{{site.time}}|
|pages|{{site.pages|size}}|
|pages[]|{title,content,dir,name,path,url,* layout,date}|
|posts|{{site.posts|size}}|
|posts[]|{output,collection:posts,url,content,id,previous:post_obj,relative_path,draft,categories,layout,author,date,title,slug,ext,tags,excerpt,next}|
|related_posts|当页面为一个post时存在|
|static_files|{{site.static_files|size}}|
|static_files[]|{path, modified_time, name, basename and extname}|
|html_pages|{{site.html_pages|size}}|
|html_pages[]|{layout,title,content,dir,name,path,url}|
|html_files|{{site.html_files|size}}|
|collections|{{site.collections|size}} _config.yml>collections>[CUSTOM_COLLECTION_NAME]|
|collections[]|{output,directory,relative_directory,files,label,docs,}|
|site.[CUSTOM_COLLECTION_NAME]|_[CUSTOM_COLLECTION_NAME]/files , obj like posts[]|
|data.*|_data/*.yml|
|documents|collections中的所有文件集合|
|site.categories.CATEGORY|The list of all Posts in category CATEGORY|
|site.tags.TAG|The list of all Posts with tag TAG|
|site.url|{{site.url}}|
|site.[CONFIGURATION_DATA]|_config.yml中定义的属性|
|site.document&#124;map:'categories'&#124;compact&#124;uniq|{{site.documents|map:'categories'|compact|uniq|inspect}} 所有的分类集合|

{{site.documents|map:'categories'|inspect}}

{% for item in site.categories %}
{{item|inspect}}
{% break; %}
{% endfor %}


site.config >> empty   
data >> _data  
data.nav >> _data.nav.yml  
static_files >> []  
documents >> [html,html]  
time
source
”destination”
”collections_dir”
”plugins_dir”
”layouts_dir”
”data_dir”
”includes_dir”
”safe”
”include”
”exclude”
”keep_files”
”encoding”
”markdown_ext”
”strict_front_matter”
”show_drafts”
”limit_posts”
”future”
”unpublished”
”whitelist”
”plugins”
”markdown”
”highlighter”
”lsi”
”excerpt_separator”
”incremental”
”detach”
”port”
”host”
”baseurl”
”show_dir_listing”
”permalink”
”paginate_path”
”timezone”
”quiet”
”verbose”
”defaults” >> _config.yml >> defaults
”liquid”:{“error_mode”,”strict_filters”,”strict_variables”},
”rdiscount”,”redcarpet”,”kramdown”,”paginate”,”livereload_port”,
”watch”,”url”


