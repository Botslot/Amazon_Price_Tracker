from bs4 import BeautifulSoup
import requests
import smtplib
import os
from dotenv import load_dotenv
from email.message import EmailMessage

load_dotenv()
my_email=os.getenv("MY_EMAIL")
password=os.getenv("PASSWORD")
to_mail=os.getenv("TO_MAIL")

headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) "
                  "AppleWebKit/537.36 (KHTML, like Gecko) "
                  "Chrome/139.0.0.0 Safari/537.36",
    "Accept-Language": "en-US,en;q=0.9,ta;q=0.8",
    }

url ="https://www.amazon.com/dp/B075CYMYK6?ref_=cm_sw_r_cp_ud_ct_FM9M699VKHTT47YD50Q6&th=1"
response = requests.get(url, headers=headers)
soup = BeautifulSoup(response.text, "html.parser")
price_data = soup.find(class_="aok-offscreen").get_text().split("$")
price = float(price_data[1].split("with")[0])
title =soup.find(id="productTitle").get_text().strip()
BUY_PRICE = 100
if price<BUY_PRICE:
    msg = EmailMessage()
    msg['Subject'] = f"{title} is now ${price}"
    msg['From'] = my_email
    msg['To'] = to_mail
    msg.set_content(f"Check the price here{url}")
    with smtplib.SMTP("smtp.gmail.com",587) as connection:
        connection.starttls()
        connection.login(my_email,password)
        connection.sendmail(msg['From'],msg['To'],msg.as_string())

