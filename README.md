# Expense_tracker-
Expense Tracker App

This is a simple Expense Tracker application developed using Streamlit, Pandas, Matplotlib, and Seaborn. It allows users to track their daily expenses, categorize them, visualize them with bar charts, and save or load expense data via CSV files.

Features

Add Daily Expenses: Input date, category, amount, and description of an expense.
View Expenses: View all recorded expenses in a table.
Save Expenses: Save the current expense data into a CSV file.
Load Expenses: Load previously saved expenses from a CSV file.
Visualize Expenses: View a bar chart that visualizes expenses by category.

Requirements

Python 3.x
Streamlit
Pandas
Matplotlib
Seaborn

How to Run

Clone this repository to your local machine.
Run the Streamlit app by executing the following command in your terminal:
streamlit run /path/to/expense_tracker.py
Replace /path/to/expense_tracker.py with the actual path to the script on your machine.

Code Explanation

Importing Libraries
import streamlit as st
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
Streamlit is used for creating the web interface.
Pandas is used for managing and manipulating the expense data in tabular form.
Matplotlib and Seaborn are used for visualizing the expense data.
Expense Data Storage
if 'expenses' not in st.session_state:
    st.session_state.expenses = pd.DataFrame(columns=['Date', 'Category', 'Amount', 'Description'])
We initialize an empty Pandas DataFrame to store expenses. This is stored in the session_state to persist data across user interactions in the app.

Adding an Expense
def add_expense(date, category, amount, description):
    new_expense = pd.DataFrame([[date, category, amount, description]], columns=st.session_state.expenses.columns)
    st.session_state.expenses = pd.concat([st.session_state.expenses, new_expense], ignore_index=True)
This function adds a new expense to the DataFrame. It takes the date, category, amount, and description of the expense as inputs.

Loading Expenses from CSV
def load_expenses():
    uploaded_file = st.file_uploader("Choose a file", type=['csv'])
    if uploaded_file is not None:
        st.session_state.expenses = pd.read_csv(uploaded_file)
The load_expenses function allows users to upload a CSV file containing expense data. The data is loaded into the expenses DataFrame.

Saving Expenses to CSV
def save_expenses():
    st.session_state.expenses.to_csv('expenses.csv', index=False)
    st.success("Expenses saved successfully!")
This function saves the current expenses in the session_state DataFrame to a CSV file named expenses.csv.

Visualizing Expenses
def visualize_expenses():
    if not st.session_state.expenses.empty:
        fig, ax = plt.subplots()
        sns.barplot(data=st.session_state.expenses, x='Category', y='Amount', ax=ax)
        plt.xticks(rotation=45)
        st.pyplot(fig)
    else:
        st.warning("No expenses to visualize!")
The visualize_expenses function creates a bar chart using Seaborn to visualize the total expenses for each category. It displays a warning message if there are no expenses to visualize.

Streamlit Layout
st.title('VISHAL EXPENSE TRACKER')
This sets the title of the app to VISHAL EXPENSE TRACKER.

Sidebar - Add Daily Expense

with st.sidebar:
    st.header('Add Daily Expense')
    date = st.date_input('Date')
    category = st.selectbox('Category', ['Meals', 'Fuel', 'Entertainment', 'Girlfriend', 'Other'])
    amount = st.number_input('Amount', min_value=0.0, format="%.2f")
    description = st.text_input('Description')
    if st.button('Add'):
        add_expense(date, category, amount, description)
        st.success('Expense added!')
This sidebar allows users to input daily expenses, including:

Date: A date picker for selecting the date.
Category: A dropdown to choose the category of the expense (Meals, Fuel, Entertainment, etc.).
Amount: A number input field for entering the expense amount.
Description: A text input field to describe the expense.
When the Add button is pressed, the expense is added to the expense list.

Sidebar - File Operations

st.header('File Operations')
if st.button('Save Expenses'):
    save_expenses()
if st.button('Load Expenses'):
    load_expenses()
In this section, users can:

Save Expenses: Save the current expense data to a CSV file.
Load Expenses: Load previously saved expense data from a CSV file.
Displaying the Expenses

st.write(st.session_state.expenses)
This displays the list of expenses in a tabular format using Pandas DataFrame.

Visualizing the Expenses

st.header('Visualization')
if st.button('Visualize Expenses'):
    visualize_expenses()
When the Visualize Expenses button is clicked, a bar chart is displayed, showing the total amount spent in each category.

File Operations

Save Expenses: Saves the current expenses to a CSV file (expenses.csv).
Load Expenses: Allows you to upload a CSV file containing previous expenses.


