---
category: literature_note  
aliases:
 - {{citekey}}
 - {{DOI}}
type: {{itemType}}
firstAuthor: {{creators[0].lastName}}
authors: 
 - {{creators[0].lastName}}
 - {{creators[1].lastName}}
 - {{creators[2].lastName}}
 - {{creators[3].lastName}}
 - {{creators[4].lastName}}
 - {{creators[5].lastName}}
 - {{creators[6].lastName}}
 - {{creators[7].lastName}}
 - {{creators[8].lastName}}
 - {{creators[9].lastName}}
 - {{creators[10].lastName}}
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
status:: {{ status }}
---

{%- for annotation in annotations %}  
{%- if annotation.imageRelativePath %}  
{%- if annotation.comment == "title" %}  
![[{{annotation.imageRelativePath }}]]  
{%- endif %}  
{%- endif %}  
{%- endfor %}

# {{title}}

**Fiche de lecture**: {% set authorCount = creators | length %} {% if authorCount == 1 %} [[👩🏽‍🔬 LITTERATURE_NOTES/READING_SHEET/RS_({{creators[0].lastName}}, {{date | format("YYYY")}})]] {% elif authorCount == 2 %} [[👩🏽‍🔬 LITTERATURE_NOTES/READING_SHEET/RS_({{creators[0].lastName}} & {{creators[1].lastName}}, {{date | format("YYYY")}})]] {% else %} [[👩🏽‍🔬 LITTERATURE_NOTES/READING_SHEET/RS_({{creators[0].lastName}} et al., {{date | format("YYYY")}})]] {% endif %}


> [!related]-  Contribution
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
> {{abstractNote}}  
> {%- endif -%}.  

> [!keywords]- 
 keywords:: {% if allTags %} {% for tag in allTags.split(', ') %} #{{tag}} {% endfor %} {% endif %}


<br>
<br>

# B. ANNOTATIONS
{% for annotation in annotations -%}
{%- if annotation.comment != "title" %}
    {%- if annotation.annotatedText -%} 
	<mark class="hltr-{{annotation.colorCategory | lower}}">"{{annotation.annotatedText | escape}}”</mark> [Page {{annotation.page}}](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.page}}&annotation={{annotation.id}})
    {%- endif %} 
    {%- if annotation.imageRelativePath -%}
    ![[{{annotation.imageRelativePath}}]] {%- endif %} 
{%- if annotation.comment %} 

{{annotation.comment}} 

<br>

{%- endif %} 
{%- endif %} 



{% endfor %}
