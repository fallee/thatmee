---
title: jekyll 参考样例
categories: [ref,jekyll]
tags: [ref,jekyll]
---

## values

### site

|name|value|
|:---:|---|
|pages|size:{{site.pages|size}} # 所有文件集合包含css和js|
|pages[page]|{title,content,dir,name,path,url,* layout,date}|
|pages.url|`{{site.pages|map:'url'|join:','|truncate:150}}`|
|static_files|{{site.static_files|size}}|
|static_files[]|{path, modified_time, name, basename and extname}|
|html_pages|size:{{site.html_pages|size}} # 输出为.html的文件集合|
|html_pages[page]|{layout,title,content,dir,name,path,url}|
|html_pages.url|`{{site.html_pages|map:'url'|join:','|truncate:150}}`|
|html_files|size:{{site.html_files|size}}|
|collections|size:{{site.collections|size}} _config.yml>collections>[CUSTOM_COLLECTION_NAME]|
|collections[collection]|{output,directory,relative_directory,files,label,docs}|
|[COLLECTION_NAME]|_config.yml:collections:[COLLECTION_NAME], _[COLLECTION_NAME]/[*file*] , 集合在_config.yml中定义,通过site.[COLLECTION_NAME]获取文件列表（同posts下的文件属性一致）, 包含在site.collections列表中|
|collections.label|map:label > {{site.collections|map:'label'|jsonify}} # 所有config中定义的集合名称|
|posts|size:{{site.posts|size}} 默认定义的collection对应_post目录|
|posts[post]|{output,collection:posts,url,content,id,previous:post_obj,relative_path,draft,categories,layout,author,date,title,slug,ext,tags,excerpt,next}|
|posts.slug|`{{site.posts|map:'slug'|join:','|truncate:150}}`|
|related_posts|当页面为一个post时存在|
|documents|size:{{site.documents|size}} collections中定义的所有集合（包含默认定义的post集合）对应的目录中的所有文件集合|
|documents.url|`{{site.documents|map:'url'|join:','|truncate:150}}`|
|tags.[TAG]|The list of all Posts with tag TAG|
|categories.[CATEGORY]|The list of all Posts in category CATEGORY|
|documents.categories|documents.categories:compact:uniq > {{site.documents|map:'categories'|compact|uniq|inspect}} # 所有的分类名称集合|
|[CONFIGURATION_DATA]|_config.yml中自定义的属性|
|data.[YML_NAME]|_data/[YML_NAME].yml _data目录中定义的yml文件中的值|
|data.nav| data.nav 在对应的 _data/nav.yml 文件中定义|
|defaults|{{site.defaults|jsonify|truncate:150}} # 默认值|
|url|{{site.url}}|
|time|{{site.time}}|
|source|{{site.source|jsonify}}|
|destination|{{site.destination|jsonify}}|
|collections_dir|{{site.collections_dir|jsonify}}|
|plugins_dir|{{site.plugins_dir|jsonify}}|
|layouts_dir|{{site.layouts_dir|jsonify}}|
|data_dir|{{site.data_dir|jsonify}}|
|includes_dir|{{site.includes_dir|jsonify}}|
|safe|{{site.safe|jsonify}}|
|include|{{site.include|jsonify}}|
|exclude|{{site.exclude|jsonify}}|
|keep_files|{{site.keep_files|jsonify}}|
|encoding|{{site.encoding|jsonify}}|
|markdown_ext|{{site.markdown_ext|jsonify}}|
|strict_front_matter|{{site.strict_front_matter|jsonify}}|
|show_drafts|{{site.show_drafts|jsonify}}|
|limit_posts|{{site.limit_posts|jsonify}}|
|future|{{site.future|jsonify}}|
|unpublished|{{site.unpublished|jsonify}}|
|whitelist|{{site.whitelist|jsonify}}|
|plugins|{{site.plugins|jsonify}}|
|markdown|{{site.markdown|jsonify}}|
|highlighter|{{site.highlighter|jsonify}}|
|lsi|{{site.lsi|jsonify}}|
|excerpt_separator|{{site.excerpt_separator|jsonify}}|
|incremental|{{site.incremental|jsonify}}|
|detach|{{site.detach|jsonify}}|
|port|{{site.port|jsonify}}|
|host|{{site.host|jsonify}}|
|baseurl|{{site.baseurl|jsonify}}|
|show_dir_listing|{{site.show_dir_listing|jsonify}}|
|permalink|{{site.permalink|jsonify}}|
|paginate_path|{{site.paginate_path|jsonify}}|
|timezone|{{site.timezone|jsonify}}|
|quiet|{{site.quiet|jsonify}}|
|verbose|{{site.verbose|jsonify}}|
|liquid|{{site.liquid|jsonify}}|
|rdiscount|{{site.rdiscount|jsonify}}|
|watch|{{site.watch|jsonify}}|
|url|{{site.url|jsonify}}|
  
  
{{site.collections[0]|jsonify}}  
{{site.collections[0].image|jsonify}}  
{{site.collections[0].all_vendors|jsonify}}  
  
### page

|name|value|
|:---:|---|
|content|# 正文内容|
|excerpt|# 正文第一段|
|title|{{page.title}} # 标题|
|url|{{page.url}} # url|
|date|{{page.date|date:'%Y-%m-%d %H:%M:%S'}} # date 定义与文件头（YYYY-MM-DD HH:MM:SS +/-TTTT）或url路径|
|id|{{page.id}} # |
|categories|{{page.categories|jsonify}} # |
|tags|{{page.tags|jsonify}} # |
|dir|{{page.dir}} # |
|name|{{page.name}} # |
|path|{{page.path}} # |
|next|{{page.next.url}} # |
|previous|{{page.previous.url}} # |
|[VAL_NAME]|# 通过yml语法定义于文件头的自定义变量|

### paginator

|name|value|
|:---:|---|
|page||
|per_page||
|posts||
|total_posts||
|total_pages||
|previous_page||
|previous_page_path||
|next_page||
|next_page_path||


{{paginator|jsonify}}
  
  