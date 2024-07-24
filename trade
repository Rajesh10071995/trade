import streamlit as st
import requests
import json

# Function to get the access token
def get_access_token(client_id, secret_key, redirect_uri, auth_code):
    url = "https://api.fyers.in/api/v2/token"
    payload = {
        "client_id": client_id,
        "secret_key": secret_key,
        "redirect_uri": redirect_uri,
        "auth_code": auth_code,
        "grant_type": "authorization_code"
    }
    headers = {
        "Content-Type": "application/json"
    }
    response = requests.post(url, data=json.dumps(payload), headers=headers)
    return response.json()

# Function to get market data
def get_market_data(access_token, symbol):
    url = f"https://api.fyers.in/api/v2/quotes/{symbol}"
    headers = {
        "Authorization": f"Bearer {access_token}",
        "Content-Type": "application/json"
    }
    response = requests.get(url, headers=headers)
    return response.json()

st.title("Fyers API Market Data")

client_id = st.text_input("Client ID")
secret_key = st.text_input("Secret Key")
redirect_uri = st.text_input("Redirect URI")
auth_code = st.text_input("Auth Code")
symbol = st.text_input("Symbol")

if st.button("Get Access Token"):
    token_data = get_access_token(client_id, secret_key, redirect_uri, auth_code)
    access_token = token_data.get("access_token")
    st.write("Access Token:", access_token)

    if st.button("Get Market Data"):
        market_data = get_market_data(access_token, symbol)
        st.json(market_data)

