pragma solidity ^0.8.0;

contract StockPriceData {
    struct StockPrice {
        uint256 price;
        uint256 timestamp;
        address submitter;
    }

    mapping(string => StockPrice[]) private stockPrices;

    event StockPriceSubmitted(
        string stockSymbol,
        uint256 price,
        uint256 timestamp,
        address indexed submitter
    );

    // Function to submit stock price data
    function submitStockPrice(string memory stockSymbol, uint256 price) public {
        StockPrice memory newPrice = StockPrice({
            price: price,
            timestamp: block.timestamp,
            submitter: msg.sender
        });

        stockPrices[stockSymbol].push(newPrice);

        emit StockPriceSubmitted(stockSymbol, price, block.timestamp, msg.sender);
    }

    // Function to get stock price data
    function getStockPrices(string memory stockSymbol) public view returns (StockPrice[] memory) {
        return stockPrices[stockSymbol];
    }
}
