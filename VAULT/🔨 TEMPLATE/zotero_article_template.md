---
category: literature_note  
aliases:
 - {{citekey}}
 - {{DOI}}
type: {{itemType}}
firstAuthor: {{creators[0].lastName}}
publication: {{publicationTitle}}
year: {{date | format("YYYY")}} 
{% set status = "unread" %}  {# Par défaut, le statut est "0" #}
{% if allTags %}
  {% for tag in allTags.split(', ') %}
    {% if tag == "0" %}
      {% set status = "unread" %}
    {% elif tag == "1" %}
      {% set status = "progress" %}
    {% elif tag == "2" %}
      {% set status = "read" %}
    {% endif %}
  {% endfor %}
{% endif %}
Authors: {% for creator in creators %}
{% if creator.creatorType == "author" %}
  - "{% if creator.name %}[[{{ creator.name }}]]{% else %}[[{{ creator.lastName }}]], {{ creator.firstName }}{% endif %}"
{% endif %}
{% endfor %}
status:: {{ status }}
---


{%- for annotation in annotations %}  
{%- if annotation.imageRelativePath %}  
{%- if annotation.comment == "title" %}  
![[{{annotation.imageRelativePath }}|1000]]  
{%- endif %}  
{%- endif %}  
{%- endfor %}

# {{title}}

**Fiche de lecture**: {% set authorCount = creators | length %} {% if authorCount == 1 %} [[👩🏽‍🔬 LITTERATURE_NOTES/READING_SHEET/RS_({{creators[0].lastName}}, {{date | format("YYYY")}})_{{citekey}}]] {% elif authorCount == 2 %} [[👩🏽‍🔬 LITTERATURE_NOTES/READING_SHEET/RS_({{creators[0].lastName}} & {{creators[1].lastName}}, {{date | format("YYYY")}})_{{citekey}}]] {% else %} [[👩🏽‍🔬 LITTERATURE_NOTES/READING_SHEET/RS_({{creators[0].lastName}} et al., {{date | format("YYYY")}})_{{citekey}}]] {% endif %}

**Lien Zotero**:: {{pdfZoteroLink}}

<br> 

> [!question]+ 
 > **Question**:: {%- for annotation in annotations %}  {%- if annotation.comment and "QUESTION" in annotation.comment|string %} {{ annotation.comment.replace("QUESTION :", "") | escape }}  {%- endif %}{%- endfor %}


> [!abstract]+  Contribution
> **Contribution**:: {%- if notes %} {{ notes[0].note }} {%- else %} {%- endif %}


<br>
<br>

# A. GENERAL INFORMATIONS

>[!Info]- Metadata
> ---
>{% for type, creators in creators | groupby("creatorType") -%}  
{%- for creator in creators -%}  
> **{{"First" if loop.first}}{{type | capitalize}}**::{%- if creator.name %} {{creator.name}}    
{%- else %} [[{{creator.lastName}}]], {{creator.firstName}}    
{%- endif %}    
{% endfor %}~   
{%- endfor %}    
> **Title**:: {{title}}    
> **Year**:: {{date | format("YYYY")}}     
> **Citekey**:: {{citekey}} {%- if itemType %}    
> **itemType**:: {{itemType}}{%- endif %}{%- if itemType == "journalArticle" %}    
> **Journal**:: *{{publicationTitle}}* {%- endif %}{%- if volume %}    
> **Issue**:: {{issue}} {%- endif %}{%- if itemType == "bookSection" %}    
> **Book**:: {{publicationTitle}} {%- endif %}{%- if publisher %}    
> **Publisher**:: {{publisher}} {%- endif %}{%- if Location %}    
> **Location**:: {{place}} {%- endif %}{%- if DOI %}     
> **DOI**:: {{DOI}} {%- endif %}  

> [!Info]- Abstract
> ---
> {%- if abstractNote %}  
> {{abstractNote|replace("  ","")}}  
> {%- endif -%}.  

> [!check]+ Keywords
 keywords:: {% if allTags %} {% for tag in allTags.split(', ') %} #{{tag|replace(" ","_")}} {% endfor %} {% endif %}


<br>
<br>


# B. ANNOTATIONS
{% for annotation in annotations -%}
{%- if annotation.comment != "title" %}
	{%- if annotation.comment == "part1" %} ## {{annotation.annotatedText | escape}}
	{%- elif annotation.comment == "part2" %} ### {{annotation.annotatedText | escape}}
	{%- elif annotation.comment == "part3" %} #### {{annotation.annotatedText | escape}}
	{%- elif annotation.comment == "part4" %} ##### {{annotation.annotatedText | escape}}
    {%- elif annotation.annotatedText -%} 
	<mark class="hltr-{{annotation.colorCategory | lower}}">"{{annotation.annotatedText | escape}}”</mark> [Page {{annotation.page}}](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.page}}&annotation={{annotation.id}})
    {%- endif %} 
    {%- if annotation.imageRelativePath -%}
    ![[{{annotation.imageRelativePath}}]] {%- endif %} 
{%- if annotation.comment != "part1" %} 
{%- if annotation.comment != "part2" %}
{%- if annotation.comment != "part3" %}
{%- if annotation.comment != "part4" %}

{%- if annotation.comment %}  

* {{annotation.comment}}

    {%- endif %} 
    
<br>

{%- endif %} 
{%- endif %} 
{%- endif %}
{%- endif %}
{%- endif %}

{% endfor %}

