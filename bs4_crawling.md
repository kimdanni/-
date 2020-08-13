```python
import pandas as pd
import urllib.request
from bs4 import BeautifulSoup
from collections import OrderedDict
import itertools
url = "http://quotes.toscrape.com/"
html = urllib.request.urlopen(url).read()
soup = BeautifulSoup(html, 'html.parser')

title = soup.find_all(class_='text')
tag = soup.find_all(class_='tags')
author = soup.find_all(class_= 'author')

tag_list = []
author_list = []
text_list = []

for i, j, z in zip(author, tag, title):
    tag_list.append(j.text)
    author_list.append(i.text)
    text_list.append(z.text)
    
unique_tag_set = set(tag_list)
unique_tag = list(unique_tag_set)

tag_list = [i.split('\n') for i in tag_list]

unique_tag = [i.split('\n') for i in unique_tag]

for i in range(len(tag_list)):
    del tag_list[i][0:3]
    del tag_list[i][-1]

for i in range(len(tag_list)):
    del unique_tag[i][0:3]
    del unique_tag[i][-1]

    
unique_author_set = set(author_list)
unique_author = list(unique_author_set)

Scrape_set = {'title':text_list,'unique tag':unique_tag,'unique author':unique_author, 'tag':tag_list, 'author':author_list}
Scrape_set1 = pd.DataFrame.from_dict(Scrape_set, orient = 'index')
Scrape_set1.transpose()
Scrape_set1.to_csv('web_ch.csv')
```


```python
Scrape_set1
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>title</th>
      <td>“The world as we have created it is a process ...</td>
      <td>“It is our choices, Harry, that show what we t...</td>
      <td>“There are only two ways to live your life. On...</td>
      <td>“The person, be it gentleman or lady, who has ...</td>
      <td>“Imperfection is beauty, madness is genius and...</td>
      <td>“Try not to become a man of success. Rather be...</td>
      <td>“It is better to be hated for what you are tha...</td>
      <td>“I have not failed. I've just found 10,000 way...</td>
      <td>“A woman is like a tea bag; you never know how...</td>
      <td>“A day without sunshine is like, you know, nig...</td>
    </tr>
    <tr>
      <th>unique tag</th>
      <td>[life, love]</td>
      <td>[edison, failure, inspirational, paraphrased]</td>
      <td>[be-yourself, inspirational]</td>
      <td>[misattributed-eleanor-roosevelt]</td>
      <td>[change, deep-thoughts, thinking, world]</td>
      <td>[humor, obvious, simile]</td>
      <td>[abilities, choices]</td>
      <td>[inspirational, life, live, miracle, miracles]</td>
      <td>[aliteracy, books, classic, humor]</td>
      <td>[adulthood, success, value]</td>
    </tr>
    <tr>
      <th>unique author</th>
      <td>Jane Austen</td>
      <td>Eleanor Roosevelt</td>
      <td>J.K. Rowling</td>
      <td>Marilyn Monroe</td>
      <td>Thomas A. Edison</td>
      <td>Albert Einstein</td>
      <td>André Gide</td>
      <td>Steve Martin</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>tag</th>
      <td>[change, deep-thoughts, thinking, world]</td>
      <td>[abilities, choices]</td>
      <td>[inspirational, life, live, miracle, miracles]</td>
      <td>[aliteracy, books, classic, humor]</td>
      <td>[be-yourself, inspirational]</td>
      <td>[adulthood, success, value]</td>
      <td>[life, love]</td>
      <td>[edison, failure, inspirational, paraphrased]</td>
      <td>[misattributed-eleanor-roosevelt]</td>
      <td>[humor, obvious, simile]</td>
    </tr>
    <tr>
      <th>author</th>
      <td>Albert Einstein</td>
      <td>J.K. Rowling</td>
      <td>Albert Einstein</td>
      <td>Jane Austen</td>
      <td>Marilyn Monroe</td>
      <td>Albert Einstein</td>
      <td>André Gide</td>
      <td>Thomas A. Edison</td>
      <td>Eleanor Roosevelt</td>
      <td>Steve Martin</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
