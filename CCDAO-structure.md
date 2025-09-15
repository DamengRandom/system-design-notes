# CCDAO Structure

I call this is a structure (skeleton) to answer the system design questions within 5 steps. Thanks for sharing [Juntao](https://www.youtube.com/@icodeit.juntao)

(From a different angle/perspective to prepare the system design interview for engineers/developers ~)

- Full name of current structure: 

  - (C)ollect information

  - (C)omponent structure

  - (D)ata Modeling

  - (A)PI design

  - (O)ptimization Strategies

## Specific Example: Typeahead (Google Search)

1. Collect information:
  - Questions: 

    - The scale of application (Is there a millions of records inside system or few thousands, how big?)

    - Devices (mobile, desktop or other devices?)

    - Is that required a prefetch and save data to local cache and then do the local frontend search or doing API requesting after typing completed?

    - Do we need to do pagination? Or only show top-pop items?

    - Error handlings? loading state tracking? reqquired?

    - Does the system need to have offline support?

    - Accessability considerations (eg: ally, keyboard navigations)?

[Personal View] Quick sumup, we always need to think-rethink and prepare the questions before starting to design the system, design = questions + think + rethink + filter/extract key points + act

2. Component structure

  - Search bar component:
    - input field: ask user to type 
    - clear button: to clear search result and re-type
    - search button: button component which is used to trigger search action 
    - web accessability support functionality

  - Results board component:
    - show the list of records
      - record component for each row (also indirectly buy yourself some time for prepare the data model in step 3, how data looks like?)
        - image (if has)
        - title
        - description
        - other metadata (if has), such as links (security considerations when opening new links)
    - pagniation (if required)
    - web accessability support functionality
  
  - Error handling component
    - loading state
    - error notifications (could be a component or a notification message)
    - web accessability support functionality (User friendly for giving proper error information to the en users)

  - State handling, like:
    - React query for fetching data before saving into store
    - after data saved into component level, using a state store (Redux, Zustand, Pinia (for Vue) and etc) to store the component required data as STATE before rendering the component contents, thats why we need loading state ~
    - headless components pattern (Check for details: [here](https://martinfowler.com/articles/headless-component.html)), generally, I would agree its good practice for the new system design. If we have exsiting pre-built components (eg: own component lib), might be a good timing to discuss with team members for the own component lib integrations. (**There is no perfect and fixed answer, but it indeed require communication between team members to figure our the most suitable solution for the design**)

[Personal View] Quick sumup, during component structure design process, we may need to ask interviewer some feedbacks after demonstrate our own undersatnding of the component part of design. Mutual communication is always important to share the opinions between interviewer and interviewee and keep design direction on the right track and coninue.

3. Data modeling

<!-- Part 1: General data structure -->
```json
{
  "data": {
    "pageInfo": { // for pagniation
      "pageNumber": "number",
      "pageSize": "number",
      "hasNext": "boolean",
      "hasPrevious": "boolean",
    },
    "records": Record[], // from below Part 2
    "createdAt": "string",
    "updatedAt": "string",
  }
}
```
<!-- Part 2: Each reocrd data structure -->
```json
{  
  "id": "string",
  "title": "string",
  "description": "string",
  "metadata": {
    "image": "string",
    "links": ["string", "multi-string"],
    // ... other metadata can be added in if required
  },
  "personalised": {
    // ... can add some personalised data as part of APi response if required
  }
}
```

[Personal View] Quick sumup, just list down how data looks like to the interviewers and confirm is this epxpected and ask if missing anything? [Require backend side how to deal with ]

4. API Design

- Restful API: GET `/api/search?query=URL_ENCODEED_QUERY&pageNumber={number}&pageSize={number}`, the frontend needs to add `URL_ENCODEED_QUERY` code logics in order to pass the correct query parameter to the backend for searching.

- GarphQL: 

  - Prepare the search query (**One of examples, might not be 100% accurate, just demo of understanding**): 

    ```graphql
    query Search($query: String!, $pageNumber: Int!, $pageSize: Int!) {
      search(query: $query, pageNumber: $pageNumber, pageSize: $pageSize) {
        pageInfo {
          pageNumber
          pageSize
          hasNext
          hasPrevious
        }
        records {
          id
          title
          description
          metadata {
            image
            links
          }
        }
      }
    }
    ```

[Personal View] Quick sumup, please mention the PROS & CONS of using different technologies for Restful API vs GaraphQL, and also ask interviwers some requirements, eg: flexibility, extend the API in future? According to different question answers and factors, to choose the most suitable solution for this system design

The details could be found via [here](./api-design.md) section `## A quick compare between different API paradigms`

5. Optimization Strategies

- Can talk different topics during this section, eg: performance (Suggest to talk as <b>higher priority</b>), observability, accessability, internationalization, offline support and so on

Eg: Performance

- Cache (frontend, gateway, backend persprectives)
- Network (race condition)
- Debouce & throttling
- memory leak issue prevention (Just find some topis you have good understanding and confidently to express to your inyterviewers ~)
- and so on ..

[Personal View] Quick sumup, just pick up some areas and talk something more specific, and trying to sell your understandings to the interviwers with some solid knowledge points and exmaples, examples are always convinceable for explaining certain concepts and also easier to ask feedbacks from interviewer side whether interviewers are able to capture your points or not ~
