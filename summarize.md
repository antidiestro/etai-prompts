Your task is to process the following JSON document containing URLs, titles and abstracts of scientific articles:

<input_document>
{{INPUT}}
</input_document>

Additionally, you have at your disposal the user-submitted query that originated the list of articles given above:

<user_query>
{{QUERY}}
</user_query>

You must output a JSON document consisting of the following fields: `title`, `clean_query`, `introduction_summary`, `key_findings`, `related_queries`, `query_answer`.

Here is how to resolve each field:

## title

A string that represents the title of the topic discussed across all articles.

## clean_query

A modified version of the user query with improved grammar and punctuation, adding connectors if necessary.

## introduction_summary

A markdown snippet, consisting of two paragraphs containing a general introduction to the overall topic discussed in the articles, generated using your general knowledge of it. They should be around 300-400 characters long. In the first paragraph, style in bold what could be considered the title of the topic.

## key_findings

Based on the knowledge found in the literature, identify up to eight key findings related to the topic at hand. These should be represented as an array of JSON objects with the following fields:

- `title`: A single sentence around 20 words long that summarizes and serves as an introduction to the finding
- `summary`: A detailed summary of the finding, around 400 characters long. Ground the summary by citing the relevant articles on every statement, in a numbered fashion, with each citation linking to the corresponding URL found in the `doi` field of the input document. The numbers should represent the order in which the articles are being cited, not the order in which they are found in the input JSON document. For example: `This is an example summary that makes a certain statement [1](https://source1.com), which is reenforced by a second one [2](https://source2.com).`

Make sure these key findings are fairly unique. It is acceptable to come up with less than eight if the literature does not seem to have enough quality to support so.

## query_answer (Optional)

If either:
a. the user-submitted query seems to be phrased as a question, in either English or Spanish (the presence of an interrogation sign is not strictly necessary), or
b. the summaries made so far do not seem to appropriately answer the query,
then include in the JSON response a `query_answer` field. This field should be a markdown snippet consisting of one or two paragraphs, each around 300 characters long, answering the specific query the user has made. The statements in the paragraphs must be cited in the same format as the `research_findings_summary` field.

## related_queries

An array containing a mixture of search terms and questions that the user can choose from to continue diving into the research.

# Important considerations

- Return all generated text in the same language as the user-submitted query.
- Return only the JSON result in the specified response, minified, and nothing else.
