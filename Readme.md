---
date updated: '2021-04-29T02:14:34+02:00'

---

Adapted from:
<https://w3c.github.io/rdf-star/cg-spec/editors_draft.html>

## Wikilink-star

The phrase:

"According to [[Bob|Alias bobby]], [[Alice]] has a job title of 'Assistant designer'."

Can be represented  using something similar to Turtle-star syntax, which uses double angle brackets to enclose a statement.

```
<< [[Alice]] has a job title 'Assistant designer' >> according to [[Bob|Alias bobby]] >>

```

Note that this statement does not assert that Alice has a job title of 'Assistant Designer'; it says that Bob has made that claim.

## RDF-star serialization

A possible serialization in RDF-star could be:

```turtle
@prefix :     <http://www.example.org/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .


:this a :Node ;
	:hasName "Readme.md" .

:Bob a :Node ;
	:hasAlias "Bobby" ;
	:hasName "Bob.md" .

:Alice a :Node ;
	:hasName "Alice.md" .

:has_job_title a rdfs:Property ; 
	rdfs:label "has job title" .

:according_to a rdfs:Property ; 
	rdfs:label "according to" .
	
:described_in a rdfs:Property ;  
	rdfs:label "described in" .

<< 
	<< :Alice :has_job_title "Assistant Designer" >> :according_to :Bob  
>> :statedBy :this .

 
```

## Turtle-star syntactic sugar

```turtle-star
@prefix :    <http://www.example.org/> .

:Alice
    :has_job_title "Assistant Designer" {| :accordingTo :Bob |} .
	
# Equivalent to
# << :Alice :has_job_title "Assistant Designer" >> :according_to :Bob .
	
```

@TODO

Example

- [ ] Enable rules

<http://eulersharp.sourceforge.net/>

```n3
PREFIX : <http://www.example.org/> 

{
    ?claim :statedBy ?something
}
=>
{
    ?something :claims ?claim .
}.

```

- [ ] Show some sparql results embedded in Obsidian.

```sparql
PREFIX : <http://www.example.org/> 

SELECT ?something WHERE {
   ?something :claims << :Alice ?property ?value >>
}
```

---

Exploration by Cristian Vasquez
