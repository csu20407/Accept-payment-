def process_payment(card_number):
    """
    Process a payment based on the card type.
    Visa starts with 4.
    Mastercard starts with 51-55 or 2221-2720.
    American Express starts with 34 or 37.
    Discover starts with 6011, 622126-622925, 644-649, 65.
    """
    
    # Get the first two digits and first four digits to determine the card type
    first_two_digits = int(card_number[:2])
    first_four_digits = int(card_number[:4])
    first_digit = int(card_number[:1])

    # Visa check: Starts with 4
    if first_digit == 4:
        return "Payment Approved: Visa"
    
    # Mastercard check: Starts with 51-55 or 2221-2720
    elif 51 <= first_two_digits <= 55 or 2221 <= first_four_digits <= 2720:
        return "Payment Approved: Mastercard"
    
    # American Express check: Starts with 34 or 37
    elif first_two_digits == 34 or first_two_digits == 37:
        return "Payment Rejected: American Express"
    
    # Discover check: Starts with 6011, 622126-622925, 644-649, 65
    elif (first_four_digits == 6011 or
          622126 <= first_four_digits <= 622925 or
          644 <= first_three_digits(card_number) <= 649 or
          first_two_digits == 65):
        return "Payment Rejected: Discover"
    
    # For any other card numbers
    else:
        return "Payment Rejected: Card type not supported"

def first_three_digits(card_number):
    return int(card_number[:3])

# Example Usage:
card_numbers = [
    "4111111111111111",  # Visa
    "5105105105105100",  # Mastercard
    "371449635398431",   # American Express
    "6011000990139424",  # Discover
]

for card in card_numbers:
    print(process_payment(card))
