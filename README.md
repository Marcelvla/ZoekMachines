# ElasticSearch for Magic the Gathering

In the 

## Regular Search
The regular search option uses the multi-match query from ElasticSearch. When you use this you can search multiple fields from your document, which is especially helpfull for our dataset, because there are a couple of information fields that are important for beign able to find the card you're looking for. Keywords are very important in cardgames. Therefore a lot of the time you would have single word queries. An example of this would be 'a card with Flying'. When using single word queries we'd like the field with the highest score, so we use the option 'best_fields' for our query. When having a query with more than just a keyword we'd like the highest score from more tdocumentshan just one field, so we use the option 'most_fields' for that. The Results are accompanied by a bar graph showing the converted mana costs of the results.

## Advanced Search

The Advanced search provides the user with the option to search cards based on multiple values. This is helpfull to the user when having a more complicated search request like "I need a red creature with a converted mana cost of 2". The advanced search gives the user the possibility to filter on the card type, colour, converted mana cost and the set the card belongs to. These kind of fields are very important to the deck building part of cardgames as it allows users build a deck with cards to play on each turn.

## Wordcloud
Since our documents are very small it's not very relevant to make a wordcloud of every single card. Therefore we have chosen to make a wordcloud for every expansion set in our dataset. Usually there is a general theme for an expansion and this will show in the wordclouds. We used tf-idf weighting to compute the importance of words for the wordcloud. Surprisingly we found that a lot of english stopwords still had pretty high tfidf scores compared to other terms, so we filtered those out leaving mostly keywords. 

## Pie chart

The pie charts provided in the notebook give insight into the type compisition of sets of cards and the finaly the type compisition of all the sets under "set". This provides insight into the kinds of decks a user could build using the sets.
For instance the "WAR" set has a high amount of "planeswalkers" and around this information decks can be build.

## Provide Faceted Search 

The Faceted search function helps the user filter the results from a simple query in order the get the right results for the information need. The funtion uses the simple query funtion to get the initial results and pandas is used to further filter the results. The user can filter on colour and converted mana cost if its enabled, this is usefull for the user with queries like "Flying red creature".

## Evaluating queries
### 1
    <topic number="1"  >
         <query>Flying creature in RVA</query>
         <description>
              Im looking for information on Flying creatures in RVA
         </description>
     </topic>

 Used simple search to evaluate the query <br />
 User 1: [R, N, R, R, R, N , R, R, N , R] <br />
 User 2: [R, N, R, R, N, R , N, R, R , R]

print(kappa(np.array([[1,1],[0,0],[1,1],[1,1],[1,0],[0,1],[1,0],[1,1],[0,1],[1,1]]))) <br />

 Kappa of this simple query is -0.143 meaning the judges disagree, Were solving this by using the advanced
 search to make sure all users get the right documents.

### 2
     <topic number="2"  >
         <query>Red cheap creatures</query>
         <description>
              user 1: Im looking for red cheap creatures for a quick deck
         </description>
         <description>
              user 2: Im looking for red cheap creatures for a late game deck
         </description>
     </topic>

 Used advanced search to evaluate the query <br />
 User 1: [R, N, R, R, R, N , R, R, N , R] <br />
 User 2: [R, N, R, R, R, R , N, R, R , R]

 print(kappa(np.array([[1,1],[0,0],[1,1],[1,1],[1,1],[0,1],[1,1],[1,1],[0,1],[1,1]]))) <br />
 Kappa of this advanced query is 0.375, acceptable but not the best. The complex nature of the tactical 
 needs of users is hard to capture in IR.

### 3
     <topic number="3"  >
         <query>Black mid-cost creatures</query>
         <description>
              Im looking for black sorceries for the mid game
         </description>
     </topic>

 Used advanced search to evaluate the query <br />
 User 1: [R, R, R, R, R, N , N, R, N , R] <br />
 User 2: [R, R, R, R, N, R , N, R, N , R]


 print(kappa(np.array([[1,1],[1,1],[1,1],[1,1],[1,0],[0,1],[0,0],[1,1],[0,0],[1,1]]))) <br />
 Kappa of this advanced query is 0.574, pretty good. 

### 4

     <topic number="4"  >
         <query>Creatures with trample in the collection</query>
         <description>
             Im looking for creatures with trample
         </description>
     </topic>

 Used simple search to evaluate the query <br />
 User 1: [R, R, N, R, R, R , N, N, N , R] <br />
 User 2: [R, R, N, R, N, R , N, N, N , R]


print(kappa(np.array([[1,1],[1,1],[0,0],[1,1],[1,0],[1,1],[0,0],[0,0],[0,0],[1,1]]))) <br />
 Kappa of this simple query is 0.855, good. The simple query seems sufficient in providing
 users with the needed documents. Recall seems lower then the other queries.

### 5

     <topic number="5"  >
         <query>White enchantments for the late game</query>
         <description>
            Im looking for white enchantments to use in the later stages of the game
         </description>
     </topic>

 Used advanced search to evaluate the query <br />
 User 1: [R, R, R, R, R, R , N, N, N , N] <br />
 User 2: [R, R, R, R, R, N , N, N, N , N]


print(kappa(np.array([[1,1],[1,1],[1,1],[1,1],[1,1],[1,0],[0,0],[0,0],[0,0],[0,0]]))) <br />
 Kappa of this simple query is 0.855, good. The advanced query seems to do the job,
 gets all the relevant documents to the top of the results.
 
 
### P@10

1: 0.7 and 0.7 <br />
2: 0.7 and 0.8 <br />
3: 0.7 and 0.7 <br />
4: 0.6 and 0.5 <br />
5: 0.6 and 0.5 <br />

making the avg p@10: 0.65
