# tnlink-bypass
https://link.tnlink.in
import time
import requests

from bs4 import BeautifulSoup 

url = "https://link.tnlink.in/TS95D7"  #@Nikhil562 {type:"string"}

def tnlink(url):
    client = requests.session()
    DOMAIN = "https://page.tnlink.in/"
    url = url[:-1] if url[-1] == '/' else url
    code = url.split("/")[-1]
    final_url = f"{DOMAIN}/{code}"
    ref = "https://usanewstoday.club/"
    h = {"referer": ref}
    resp = client.get(final_url,headers=h)
    soup = BeautifulSoup(resp.content, "html.parser")
    inputs = soup.find_all("input")
    data = { input.get('name'): input.get('value') for input in inputs }
    h = { "x-requested-with": "XMLHttpRequest" }
    time.sleep(8)
    r = client.post(f"{DOMAIN}/links/go", data=data, headers=h)
    try:
        return r.json()['url']
    except: return "Something went wrong :("

# ---------------------------------------------------------------------------------------------------------------------

print(tnlink(url))
