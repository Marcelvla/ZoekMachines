# ElasticSearch for Magic the Gathering

In the 

## Regular Search
The regular search option uses the multi-match query from ElasticSearch. When you use this you can search multiple fields from your document, which is especially helpfull for our dataset, because there are multiple  

## Advanced Search


## Wordcloud
Since our documents are very small it's not very relevant to make a wordcloud of every single card. Therefore we have chosen to make a wordcloud for every expansion set in our dataset. Usually there is a general theme for an expansion and this will show in the wordclouds. We used tf-idf weighting to compute the importance of words for the wordcloud. 

## Pie chart



## Provide Faceted Search 



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
