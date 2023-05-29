# StocksTerminal - SE_Project

![](https://s40424.pcdn.co/in/wp-content/uploads/2022/07/info-systems.jpg.webp)

---

**Software Engineering Project:** CLI Stock Data Manager

**Collaborators:** Max Franklin `&&` Noam Ben Simon

---

> Needs Being Met:

Ease of access to current and live stock data at a moment's notice.

> Who would use it?

Anyone from brokers trying to get a quick breakdown of a certain stock to everyday people trying to educate themselves on current public finances, and software engineers trying to simplify stock data.

This software can be particularly useful for automation. For example, someone can make a bash script that can send email notifications when certain stock data triggers a defined threshold.

> What functions are provided?

This software will be capable of retrieving all sorts of data with regard to stock ticker symbols. The data can be provide as a querry - whereby a single request is sent for the current market data for a stock (or stocks), or live data - which will continue to update the data in the CLI every decided interval.

It will also allow for summarizing tools in order to isolate and prioritize the most wanted information. Additionally, there will be functionality to querry multiple stock tickers and get a list of formatted data for each.

> Why?

To simplify and organize the information-getting process for stock data.

> How?

1.  Run the program .jar file (or directly through program files).

2.  make a call to the program using "stock" as the first item of your args.

3.  use one of the following commands to call and retrieve data:

        (a) "help" - prints a list of available commands, requests, and options,
        as well as a short description of each, akin to this list.

        (b) "[stock_symbol(s)] [request(s) flag(s)]"
            - executes the given command on the stock symbol(s) provided
            - separate symbols and requests with a space. Example provided:
            "aapl amzn -pov" - fetches the price, open
            price, and volume for aapl and amzn (empty
            request status assumes current)
            ---
            request flags and their uses:
                No specification / "" - assumes all other requests (same as "-cehloprtv")
                (All the following go after a "-")
                1. open / "o" - day's open price
                2. high / "h" - day's high price
                3. low / "l" - day's low price
                4. price / "e" - current price
                4. volume / "v" - stock volume
                5. latest trading day / "t" - last day that trading     was available
                6. previous close / "p" - the previous trading  day's closing price
                7. change / "c" - change in price since day's open
                8. change in percent / "r" - change in price since day's open represented as a percentage.

        (c) "clear" - clears the stock-history for refreshing data

        (d) "refresh" - gets the last stocks (up to 10) and requests all information offered on them.

        (e) "remove [stock_symbol(s)]" - removes the listed stock(s) from the data storage units. No listed stock will just delete the most recent stock symbol added.

        (f) "history" - prints all stocks that have been requested that have not been removed.

        (g) "Live [stock_symbol]" (capital "L") - gives a live feed of a specific stock.

        (h) "quit" - leaves the program.

The ideal experience using this product is straightforward: use the "help" or read the code in order to understand the commands, then apply them as you wish.

---

> Ideas/Functionality:

-   Help; Help (get help)
-   Query; Commands to get data (specify wanted data)
-   Clear; Clears stock cache
-   Refresh; Updates prices for a certain amount of stocks
-   Remove; Removes a stock from the cache
-   History; lists all stocks ever requested
-   Live; Live command (updates info every certain amount of time)
-   Quit; Exits the program

> Stock data we can get:

1.  symbol
2.  open
3.  high
4.  low
5.  price
6.  volume
7.  latest trading day
8.  previous close
9.  change
10. change percent

---

![](https://media.istockphoto.com/id/1148438339/photo/data-structure-and-information-tools-for-networking-business.jpg?b=1&s=170667a&w=0&k=20&c=d7hRfsaF-CZ3F8CblVGZa26uN3veIJJRcsny0ZIxZ9M=)

---

**Software Engineering Project:** CLI Stock Data Manager - Stage 2

**Collaborators:** Max Franklin `&&` Noam Ben Simon

---

**Data Structures:**

We will use a combination of custom classes and data structures to use and store our program.

We will also have a general "brain" that is used for the call and response of commands and requests.

**Custom Classes**

-   "Stock" - when a new stock ticker symbol is called, a new class of type "Stock" will be instantiated, with the symbol as the main identifier.

    -   this stock object will also be the main holder of data for that given stock. For example, "Stock" of type "AAPL" will hold the information requested for Apple's stock, and will refresh according to requests by the user.

-   "Logic" - the brains of the operation. Will do all necessary calls to the "Data" class and organize as well as instantiate stocks and infromation calls.

-   "Data" - Holds the references to the objects and calls within it. Added mostly to clean up and simplify the work of the "Logic" class, but will also serve an important function in hosting and updating the data calls.

**Variables and Data Structures**

_For "Stock"_

-   String: the symbol of the stock.
-   String(s): each request will have its own associated String for that information returned.
    -   This will be concatenated (or not) and returned by request of the user.
-   Long: holds the last time accessed/used for a given stock.

_For "Logic"_

-   String Array: all things passed in from args. This will be broken down into the following:
    -   String Array: stores the Stock symbols passed in.
    -   String Array: stores the arguments/commands passed in.
    -   Character Array: stores the array of flags for the actual requests of a given command (if there exist any).
-   String: the output will be formatted and concatenated into one string which will then be printed at CMD.

_For "Data"_

-   MinHeap: storage for cached stocks, which will cap at 10, and then remove the least-recently used stock and remove it from the cache.
-   ArrayList: Used to take minHeap and order it alphabetically before returning cached items' requests.
