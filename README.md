# Stock-Buy-Sell-to-Maximize-Profit
Given a array of numbers representing the stock prices of a company in chronological order, write a function that calculates the maximum profit you could have made from buying and selling that stock once. You must buy before you can sell it.  For example, given [9, 11, 8, 5, 7, 10], you should return 5, since you could buy the stock at 5 dollars and sell it at 10 dollars


#include <bits/stdc++.h>
using namespace std;
 
// Function to return the maximum profit that can be made after buying and selling the given stocks
int maxProfit(int price[], int start, int end)
{
 
    // If the stocks can't be bought
    if (end <= start)
        return 0;
 
    // Initialise the profit
    int profit = 0;
 
    // The day at which the stock
    // must be bought
    for (int i = start; i < end; i++) {
 
        // The day at which the
        // stock must be sold
        for (int j = i + 1; j <= end; j++) {
 
            // If byuing the stock at ith day and
            // selling it at jth day is profitable
            if (price[j] > price[i]) {
 
                // Update the current profit
                int curr_profit = price[j] - price[i]
                                  + maxProfit(price, start, i - 1)
                                  + maxProfit(price, j + 1, end);
 
                // Update the maximum profit so far
                profit = max(profit, curr_profit);
            }
        }
    }
    return profit;
}
 
// Driver code
int main()
{
    int price[] = { 100, 180, 260, 310, 40, 535, 695 };
    int n = sizeof(price) / sizeof(price[0]);
 
    cout << maxProfit(price, 0, n - 1);
 
    return 0;
}
