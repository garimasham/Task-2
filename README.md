import yfinance as yf

def get_stock_price(ticker):
    stock = yf.Ticker(ticker)
    current_price = stock.history(period="1d")['Close'][0]
    return current_price

def add_stock(portfolio, ticker, shares):
    ticker = ticker.upper()
    if ticker in portfolio:
        portfolio[ticker]['shares'] += shares
    else:
        portfolio[ticker] = {'shares': shares}
    return portfolio

def display_portfolio(portfolio):
    print("\nYour Stock Portfolio:")
    total_value = 0.0
    for ticker, data in portfolio.items():
        current_price = get_stock_price(ticker)
        value = data['shares'] * current_price
        total_value += value
        print(f"{ticker}: {data['shares']} shares at ${current_price:.2f} per share | Total Value: ${value:.2f}")
    print(f"\nTotal Portfolio Value: ${total_value:.2f}")

def stock_portfolio_tracker():
    portfolio = {}
    while True:
        print("\nOptions:")
        print("1. Add a stock to your portfolio")
        print("2. Display your portfolio")
        print("3. Exit")
        choice = input("Choose an option: ")

        if choice == "1":
            ticker = input("Enter stock ticker symbol: ")
            shares = int(input("Enter the number of shares: "))
            portfolio = add_stock(portfolio, ticker, shares)
        elif choice == "2":
            display_portfolio(portfolio)
        elif choice == "3":
            print("Exiting the portfolio tracker. Goodbye!")
            break
        else:
            print("Invalid choice, please select a valid option.")

if __name__ == "__main__":
    stock_portfolio_tracker()
