Dataset on kaggle with detailed description: : https://www.kaggle.com/retailrocket/ecommerce-dataset

The events file contains time, user, item information and what event happens (i.e., view, add to cart, buy), so there's no explicit ratings. I build the rating matrix by assigning different weights to these three events. 

I apply three general approaches for recommendation:

1. For a new user without any history, recommend the most popular items.

2. Recommend similar items if a user choose certain item. To find a 'similar item', I generate two ways:
  - Since some of items have category id and parent id, I recommend two most popular other items under the same category id. If there are fewer than two items under the same category id then give the full list. 
  - Many of items do not have categoy id, or it is the only product under the category id. To solve this problem, I take the time that user views/adds/buys items into consideration. According to our shopping habbit, items viewed together are most likely to be the substitutes or complements. So given an item viewed by a user, I find other items that other users view/buy/add to cart within a certain time range as that user views/buys/adds to cart that item.
  
3. Recommend based on the rating matrix. I use ALS (Alternating Least Squares) for matrix factorization. However, the result score is far away from the original rating I create. Maybe without a reliable system that assigns weights to different events, ALS will fail to produce desirable results.
  
