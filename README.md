#include <iostream>
#include <cmath>
#include <string>


enum MembershipLevel {
    NONE,
    BRONZE,
    SILVER,
    GOLD
};

double applyDiscount(double totalPrice, MembershipLevel level) {
    switch (level) {
    case BRONZE:
        return totalPrice * 0.95;  
    case SILVER:
        return totalPrice * 0.90; 
    case GOLD:
        return totalPrice * 0.85;  
    default:
        return totalPrice;         
    }
}

int main() {
    double totalPrice = 0.0; 
    char addMoreItems = 'n'; 
    do {
        double itemPrice;
        std::cout << "Enter the price of the item: ";
        std::cin >> itemPrice;    
        while (std::cin.fail()) {
            std::cin.clear();  
            std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n'); 
            std::cout << "Invalid input. Please enter a valid price: ";
            std::cin >> itemPrice;
        }
   totalPrice += itemPrice;
        std::cout << "Do you want to add another item? (y/n): ";
        std::cin >> addMoreItems;

  while (addMoreItems != 'y' && addMoreItems != 'n' && addMoreItems != 'Y' && addMoreItems != 'N') {
            std::cout << "Invalid input. Please enter 'y' for yes or 'n' for no: ";
            std::cin >> addMoreItems;
        }
    } while (addMoreItems == 'y' || addMoreItems == 'Y'); 
    int membershipInput;
    std::cout << "Enter your membership level (0 = NONE, 1 = BRONZE, 2 = SILVER, 3 = GOLD): ";
    std::cin >> membershipInput;
    while (std::cin.fail() || membershipInput < 0 || membershipInput > 3) {
        std::cin.clear(); 
        std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n'); 
        std::cout << "Invalid input. Please enter 0 for NONE, 1 for BRONZE, 2 for SILVER, or 3 for GOLD: ";
        std::cin >> membershipInput;
    }
    MembershipLevel userLevel = static_cast<MembershipLevel>(membershipInput);
    double finalPrice = applyDiscount(totalPrice, userLevel);
    std::cout << "The final price after discount is: $" << finalPrice << std::endl;
    return 0;
}
