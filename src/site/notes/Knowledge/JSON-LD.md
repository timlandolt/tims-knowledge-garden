---
{"dg-publish":true,"permalink":"/knowledge/json-ld/","tags":["webdevelopement","json","seo"]}
---

---

>[!faq]  = JavaScript Object Notation for Linked Data

JSON-LD allows us to add semantic information to JSON that's missing normally.
It is used to provide structured data to search engines. This enables them to better find a matching result for a search query, but it also helps to display fancy stuff on the results page.

**Example:**
```json
<script type="application/ld+json">
 {
"@context" : "https://schema.org",
"@type" : "Article",
"name" : "JSON-LD and SEO",
"author" : {
"@type" : "Person",
"name" : "John Doe"
},
"datePublished" : "2020-10-05",
"articleBody" : "JSON-LD can improve your site’s SEO performance because it helps search engines understand what a page is about. It also helps your site stick out in the SERPs, helping to improve your CTR.\nMajor search engines like Google encourage SEO specialists to use JSON-LD to improve their performance.",
"publisher" : {
"@type" : "Organization",
"name" : "CompanyABC"
  }
}
</script>
```

Google has made a helper for this structured data: [Structured Data Markup Helper - Search Console Help](https://support.google.com/webmasters/answer/3069489)
