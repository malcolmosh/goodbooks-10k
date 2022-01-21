# goodbooks-10k EXPANSION PACK

This is an extended version of the [Goodbooks 10k dataset](https://github.com/zygmuntz/goodbooks-10k), originally scraped from the Goodreads API in September 2017 by Zygmunt Zając. **The biggest advantage of this new version that it adds a text description field for 9943 of the 10 000 titles.** Please consult the original repository for additional information on the original files. 

Additional fields have been added to the original books.csv file via two strategies: 
* Pulling attributes from cross-referenced titles in the [Best Books Ever Dataset](https://zenodo.org/record/4265096#.YesDbi3pNB0), collected from the Goodreads website in Fall 2020 by Lorena Casanova Lozano and Sergio Costa Planells. From what I gather, they used the Selenium package to parse book webpages. 

* For the 1833 books missing from the above dataset, extended fields were scraped with the Goodreads api in October 2021. Although this API has officially been retired, I was able to find a developer key online that still worked. 

The four new fields added to the original books.csv file are : 
* `description` : a free text summarizing the book's content. On average the description is 900 characters long, with 95% of book descriptions counting less than 1797 characters. This column is 99,43% complete.
* `pages` : the total page count. This column is 99.27% complete. 
* `publishDate` : the publication date. This column is 99.92% complete.
* `genres` :  the genre tags taken from the top shelves users have assigned to a book. Only the main Goodreads genres have been retained. On average, there are 4.7 genres per title, with 75% of books containing 6 genres or less. This column is 100% complete.

The two updated fields integrated in this version are :
* `authors` : a newly scraped list of all book contributors. This can include illustrators and collaborators. This column is 100% complete. 
* `language_code` : abbreviated language tags for all books, computed by scanning the book titles with the langid package. This column is 100% complete. 

# Importing the file

```
import pandas as pd
from ast import literal_eva
 
books_df = pd.read_csv('https://raw.githubusercontent.com/malcolmosh/goodbooks-10k/master/books_enriched.csv', index_col=[0], converters={"genres": literal_eval})
```


