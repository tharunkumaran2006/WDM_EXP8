### EX8 Web Scraping On E-commerce platform using BeautifulSoup
### DATE: 17.10.2025
### NAME : THARUN V K
### REGISTER NUMBER : 212223230231
### AIM: To perform Web Scraping on SnapDeal using (beautifulsoup) Python.
### Description: 
<div align = "justify">
Web scraping is the process of extracting data from various websites and parsing it. In other words, it’s a technique 
to extract unstructured data and store that data either in a local file or in a database. 
There are many ways to collect data that involve a huge amount of hard work and consume a lot of time. Web scraping can save programmers many hours. Beautiful Soup is a Python web scraping library that allows us to parse and scrape HTML and XML pages. 
One can search, navigate, and modify data using a parser. It’s versatile and saves a lot of time.
<p>The basic steps involved in web scraping are:
<p>1) Loading the document (HTML content)
<p>2) Parsing the document
<p>3) Extraction
<p>4) Transformation

### Procedure:

1) Import necessary libraries (requests, BeautifulSoup, re, matplotlib.pyplot).
2) Define convert_price_to_float(price) Function: to Remove non-numeric characters from a price string and convert it to a float.
3) Define get_amazon_products(search_query) Function: to Scrape Amazon for product information based on the search query.
4) Fetch and parse the HTML content then Extract product names and prices from the search results and Sort product information based on converted prices in ascending order.
5) Return sorted product data as a list of dictionaries.
6) Call get_amazon_products(search_query) to get product data based on the user's search query.
7) Check if products are found; if not, display "No products found."
8) Visualize Product Data using a Bar Chart

### Program:
```PYTHON
import requests
from bs4 import BeautifulSoup


def get_snapdeal_products(search_query):
  url = f"https://www.snapdeal.com/search?keyword={search_query.replace(' ', '%20')}"
  headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) "
                  "AppleWebKit/537.36 (KHTML, like Gecko) "
                  "Chrome/126.0.0.0 Safari/537.36",

}
  response = requests.get(url, headers=headers)
  products_data = []
  if response.status_code == 200:
    soup = BeautifulSoup(response.text, "html.parser")
    products = soup.find_all("div", {"class": "product-tuple-listing"})

    for product in products:
      title = product.find("p", {"class": "product-title"}).text.strip()
      price = product.find("span", {"class": "product-price"}).text.strip()
      reviews_element = product.find("span", {"class": "product-rating-count"})
      no_of_reviews = reviews_element.text.strip() if reviews_element else "N/A"
      discount = product.find("div", {"class": "product-discount"}).text.strip()
      rating = product.find("div", {"class": "filled-stars"})
      product_rating = rating['style'].split(';')[0].split(':')[-1] if rating else None

      products_data.append({
        "Name": title,
        "Price": price,
        "Number Of Reviews": no_of_reviews,
        "Discount": discount,
        "Rating": product_rating
      })

      print(f"Product Name: {title}")
      print(f"Price: {price}")
      print(f"Number of Reviews: {no_of_reviews}")
      print(f"Discount: {discount}")
      print(f"Rating: {product_rating}")
      print("-" * 50)

  else:
    print("Failed to retrieve products.")
  return products_data

search_query = input("Enter your search query: ")
products_data = get_snapdeal_products(search_query)

```

### Output:
<img width="777" height="927" alt="Screenshot 2025-10-17 at 11 44 58 AM" src="https://github.com/user-attachments/assets/d8f3881f-7cd2-4ed4-9468-fe9b33635bfb" />


### Result:
Thus the product data from snapdeal has been scraped sucessfully using beautiful soup in python.
