# Binance Module 

## Binance.h

    Type Definitions
 
    typedef union json_h 
    {
        char *raw_json_data;
        int error;
    } JSON;

    Coin Names

    #define BTCUSDT 1
    #define ETHUSDT 2
    ...

    Interval

    #define M15 1
    #define M30 2
    ...

    #define H1 10
    #define H4 11
    ...

    #define D1 20
    #define D3 21
    ...


    Error Handling

    #define E_INVALID_PARAM         (-1)
    #define E_REQUEST_TIMEOUT       (-2)
    #define E_DATA_CORRUPTED        (-3)
    

    

### Private Functions

`static int init_socket(void);`

Initilizes a new socket , bind it to binance api and returns socket file descriptor.

#### Possible Errors

*   Socket may not be initilized
*   Binance api may not respond
*   Socket may not be binded to binance api

`static JSON request(int coin_name, int period,int candle_count ...)`

Send get request to binance api through socket returned by `get_request_socket` fetch the coin data as .json file. Other public `get` prefixed functions are wrapper for this function.

#### Return Value

On success , returns `raw_json_data`.

On error , `returns error`.

#### Possible Errors


*   Request timeout.
*   Json data corrupted   



### Public Functions

`JSON get_klines_of(int coin_name, int period, int candle_count);`

! Wrapper for `request()` function

Internally uses `request()` function for fetching sequential candle data. *Does not fetch historical data!*

#### Return Value

On success , returns `raw_json_data`.
On failure , returns `error`.

#### Possible Errors

*   Invalid parameters.

`JSON get_current_value_of(int coin_name);`

! Wrapper for `request()` function

Internally uses `request()` function for fetching current coin price and volume data.

#### Return Value

On success , returns `raw_json_data`.
On failure , returns `error`.

#### Possible Errors

*   Invalid parameters.


