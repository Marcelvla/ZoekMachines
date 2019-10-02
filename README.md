# ElasticSearch for Magic the Gathering

## Regular Search
Search as we know it from Google. Give a result page (SERP), with links to the documents and some description of each hit.

## Advanced Search
Advanced search. Let a user be able to search in several fields, also in several fields simulteanously. Queries like "return articles with a title about XXX and which are about YYY in the period ZZZ" should be possible. If you do not have timestamps in your data, then you must have some other facet(s) on which can be filtered.

## Wordcloud
You can use several techniques to get rid of high frequency, but meaningless words: of course IDF, but also mutual information (see 13.5.1), or of course the technique from the paper by Kaptein et al on wordclouds.

## Pie chart
Give next to a traditional list of results, a timeline in which you indicate how many hits there are over time. This can only be done if your "documents" have timestamps. See Google trends for an example. This is of course, simply a histogram of the number of hits per time period. If you do not have timestamps, do something else with a fancy graphic.

## Provide Faceted Search 
next to the traditional list of results. For the "Reuters" collection, use the Category information as facet values. See this example.

## Evaluating queries

<topic number="1"  >
    <query>Flying creature in RVA</query>
    <description>
         Im looking for information on Flying creatures in RVA
    </description>
</topic>

Used simple search to evaluate the query
User 1: [R, N, R, R, R, N , R, R, N , R]
User 2: [R, N, R, R, N, R , N, R, R , R]

print(kappa(np.array([[1,1],[0,0],[1,1],[1,1],[1,0],[0,1],[1,0],[1,1],[0,1],[1,1]])))

Kappa of this simple query is -0.143 meaning the judges disagree, Were solving this by using the advanced
search to make sure all users get the right documents.


<topic number="2"  >
    <query>Red cheap creatures</query>
    <description>
         user 1: Im looking for red cheap creatures for a quick deck
    </description>
    <description>
         user 2: Im looking for red cheap creatures for a late game deck
    </description>
</topic>

Used advanced search to evaluate the query
User 1: [R, N, R, R, R, N , R, R, N , R]
User 2: [R, N, R, R, R, R , N, R, R , R]

print(kappa(np.array([[1,1],[0,0],[1,1],[1,1],[1,1],[0,1],[1,1],[1,1],[0,1],[1,1]])))
Kappa of this advanced query is 0.375, acceptable but not the best. The complex nature of the tactical 
needs of users is hard to capture in IR.

<topic number="3"  >
    <query>Black mid-cost creatures</query>
    <description>
         Im looking for black sorceries for the mid game
    </description>
</topic>

Used advanced search to evaluate the query
User 1: [R, R, R, R, R, N , N, R, N , R]
User 2: [R, R, R, R, N, R , N, R, N , R]


print(kappa(np.array([[1,1],[1,1],[1,1],[1,1],[1,0],[0,1],[0,0],[1,1],[0,0],[1,1]])))
Kappa of this advanced query is 0.574, pretty good. 

<topic number="4"  >
    <query>Creatures with trample in the collection</query>
    <description>
        Im looking for creatures with trample
    </description>
</topic>

Used simple search to evaluate the query
User 1: [R, R, N, R, R, R , N, N, N , R]
User 2: [R, R, N, R, N, R , N, N, N , R]


print(kappa(np.array([[1,1],[1,1],[0,0],[1,1],[1,0],[1,1],[0,0],[0,0],[0,0],[1,1]])))
Kappa of this simple query is 0.855, good. The simple query seems sufficient in providing
users with the needed documents. Recall seems lower then the other queries.

<topic number="5"  >
    <query>White enchantments for the late game</query>
    <description>
       Im looking for white enchantments to use in the later stages of the game
    </description>
</topic>

Used advanced search to evaluate the query
User 1: [R, R, R, R, R, R , N, N, N , N]
User 2: [R, R, R, R, R, N , N, N, N , N]


print(kappa(np.array([[1,1],[1,1],[1,1],[1,1],[1,1],[1,0],[0,0],[0,0],[0,0],[0,0]])))
Kappa of this simple query is 0.855, good. The advanced query seems to do the job,
gets all the relevant documents to the top of the results.
