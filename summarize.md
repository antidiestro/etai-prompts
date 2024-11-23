Your task is to process the following JSON document containing URLs, titles and abstracts of scientific articles:

<input_document>
{{INPUT}}
</input_document>

Additionally, you have at your disposal the user-submitted query that originated the list of articles given above:

<user_query>
{{QUERY}}
</user_query>

You must output a JSON document consisting of the following fields: `title`, `introduction_summary`, `research_findings_summary`, `query_answer`.

Here is how to resolve each field:

## title

A string that represents the title of the topic discussed across all articles.

## introduction_summary

A markdown snippet, consisting of two paragraphs containing a general introduction to the overall topic discussed in the articles, generated using your general knowledge of it. They should be around 300-400 characters long. In the first paragraph, style in bold what could be considered the title of the topic.

## research_findings_summary

A markdown snippet, consisting of four paragraphs based on the knowledge found in the articles, each one detailing an area of study and its related main findings. They should be around 500-600 characters long. At the start of each one of these paragraphs, mention the area of study as a short phrase in bold, separated by the rest of the content with a period.
Ground these summaries by citing the relevant articles on every statement, in a numbered fashion, with each citation linking to the relevant URL found in the "doi" field of the input document. The numbers should represent the order in which the articles are being cited, not the order in which they are found in the input.
For example: `This is an example summary that makes a certain statement [1](https://source1.com), which is reenforced by a second one [2](https://source2.com).`

## query_answer (Optional)

If the summaries made so far do not seem to appropriately answer the user-submitted query, include in the JSON response a `query_answer` field. This field should be a markdown snippet consisting of one or two paragraphs, each around 300 characters long, answering the specific query the user has made. The statements in the paragraphs must be cited in the same format as the `research_findings_summary` field.

# Important considerations

- Return all generated text in the same language as the user-submitted query.
