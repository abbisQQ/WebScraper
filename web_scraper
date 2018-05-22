from bs4 import BeautifulSoup
import requests
from PIL import  Image
from io import BytesIO
import os


def image_search():
    search = input("Search for: ")
    dir_name = search.replace(" ", "_").lower()
    params = {"q": search}

    if not os.path.isdir(dir_name):
        os.makedirs(dir_name)

    r = requests.get("https://wwww.bing.com/images/search", params=params)
    soup = BeautifulSoup(r.text, "html.parser")
    links = soup.find_all("a", {"class": "thumb"})

    for item in links:
        try:
            img_obj = requests.get(item.attrs["href"])
            print("Getting item: ", item.attrs["href"])
            title = item.attrs["href"].split("/")[-1]

            try:
                img = Image.open(BytesIO(img_obj.content))
                img.save("./" + dir_name + "/" + title, img.format)
                print(" Image saved")
            except:
                print("Count not save the image")
        except:
            print("Could not request image")


image_search()
