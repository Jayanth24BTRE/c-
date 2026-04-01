#include <iostream>
#include <algorithm>
using namespace std;

struct Item {
    int value, weight;
};

// Comparator to sort items by value/weight ratio
bool compare(Item a, Item b) {
    double r1 = (double)a.value / a.weight;
    double r2 = (double)b.value / b.weight;
    return r1 > r2;
}

double fractionalKnapsack(int W, Item arr[], int n) {
    sort(arr, arr + n, compare);

    double totalValue = 0.0;

    for (int i = 0; i < n; i++) {
        if (arr[i].weight <= W) {
            // Take full item
            W -= arr[i].weight;
            totalValue += arr[i].value;
        } else {
            // Take fraction of item
            totalValue += arr[i].value * ((double)W / arr[i].weight);
            break;
        }
    }

    return totalValue;
}

int main() {
    int n, W;
    cout << "Enter number of items: ";
    cin >> n;

    Item arr[n];
    cout << "Enter value and weight of items:\n";
    for (int i = 0; i < n; i++) {
        cin >> arr[i].value >> arr[i].weight;
    }

    cout << "Enter capacity of knapsack: ";
    cin >> W;

    cout << "Maximum value = " << fractionalKnapsack(W, arr, n);

    return 0;
}