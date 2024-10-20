# Bank Transaction Documentation

This guide explains how to use the `BankTransaction` class from the `ipakyuli.transfer` module for creating, confirming, and canceling bank transfers.

## Installation

Ensure that you have installed the required dependencies for `ipakyuli.transfer`. If it's part of a package, you can install it using:

```bash
pip install ipakyuli
```
## Bank Authentication
Before initiating a transaction, you'll need to authenticate with the bank's API by providing necessary credentials like API URL, login, password, and cash box ID.

Example Authentication Data
```python
bank_auth = {
    "api_url": "https://example-api-url.com",  # Replace with the actual API URL
    "login": "your_login",                     # Your login credentials
    "password": "your_password",               # Your password
    "cash_box_id": "your_cash_box_id"          # Cash box ID provided by the bank
}
```
## Card Data
Card information should be provided in a dictionary containing the PAN (card number) and expiry date.

```python
card_data = {
    "pan": "8600123412341234",  # Example card number (PAN)
    "expiry": "2509"            # Expiry date in YYMM format
}
```

## Bank Transaction

To initiate a bank transaction, you'll use the BankTransaction class, passing in the card data and authentication credentials.

```python
from ipakyuli.transfer import BankTransaction

# Initialize the BankTransaction instance
bank = BankTransaction(card_data=card_data, **bank_auth)

```
## Transfer Creation
To create a new transfer, provide the amount, order ID, and a description of the payment.
```python
transfer_data = {
    "amount": 5000.0,           # Amount in the local currency
    "order_id": "3",            # Unique ID for the order
    "desc": "payment description" # Description of the payment
}

# Create a new transfer
bank.transfer_create(**transfer_data)
```
## Transfer Confirmation
After creating a transfer, you can confirm it using the confirmation code sent by the bank.

```python
# Confirm the transfer using the confirmation code
bank.transfer_confirm(code="1234")
```

## Transfer Cancellation
If you need to cancel the transfer for any reason, you can do so using the transfer_cancel method
```python
# Cancel the transfer
bank.transfer_cancel()
```
## Example Workflow
Here's an example of how the full transaction process works:

```python
from ipakyuli.transfer import BankTransaction

# Authentication credentials and card data
bank_auth = {
    "api_url": "https://example-api-url.com",
    "login": "your_login",
    "password": "your_password",
    "cash_box_id": "your_cash_box_id"
}

card_data = {
    "pan": "8600123412341234",  # Example card number (PAN)
    "expiry": "2509"            # Expiry date in YYMM format
}

# Initialize the BankTransaction instance
bank = BankTransaction(card_data=card_data, **bank_auth)

# Create a new transfer
transfer_data = {
    "amount": 5000.0,
    "order_id": "3",
    "desc": "payment description"
}
bank.transfer_create(**transfer_data)

# Confirm the transfer
bank.transfer_confirm(code="1234")

# Cancel the transfer if needed
bank.transfer_cancel()
```