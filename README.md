print('BLACK COFFEE PYTHON STORE, by Furukawa\n')

print('\n\tWelcome to BLACK COFFEEs PYTHON STORE!\n')
print('''
      
          /     /     /
        /     /     /
        /     /     /                    __        __        _
    .----------------------             |  \      /  \      / \      |\  /|
   |                       )___         |__/     /         /   \     | \/ |
   |   |       |    | | |  |__ )        |   \    \         |___|     |    |
   |  -+-     -+-   | | |  | | |        |___/  x  \__/  x  |   |  x  |    |  x
   /   |       |    | | |  |_| |
  /        /\       \ |    |___) 
 /_               __ \_____)  
    \            /
     \  /\  /\  /
      \/  \/  \/
      
      ''')

product_list = [
    ('UNTITLED CD', 10),
    ('QUEIMANDO PONTES CD', 10),
    ('QMND-PNTS - THE REMIXES VOL 1 CD', 10),
    ('WR BRN 2 SLW - GREATEST HITS VINYL RECORD 180g', 25),
    ('T-SHIRT 3FLCHS', 25),
    ('T-SHIRT DEAD!', 25),
    ('T-SHIRT PRATIQUE O QUE PREGA', 25),
    ('SHORTS TACTEL BxCxAxMx', 25),
    ('BLACK COFFEE TRUCKER HAT', 20),
    ('BLACK COFFEE CAP', 15),
    ('BLACK COFFEE HOODIE', 50),
    ('BLACK COFFEE SWEATSHIRT', 40),
    ('BLACK COFFEE LIGHTER', 5),
    ('BLACK COFFEE GRINDER', 4),
    ('BLACK COFFEE SMOKING SILK', 5),
    ('BLACK COFFEE STICKER PACK', 5),
    ('SOCKS WR BRN 2 SLW', 20),
    ('BLACK COFFEE GUITAR PICK', 1),
    ('BLACK COFFEE PRINT', 10),
    ('BLACK COFFEE POSTER', 10),
    ('BLACK COFFEE STENCIL KIT', 5),
    ('BLACK COFFEE MUG', 15),
    ('BLACK COFFEE CUP', 10),
    ('BLACK COFFEE KEYCHAIN', 10),
    ('BLACK COFFEE ECOBAG', 30),
    ('BLACK COFFEE JACKET', 60),
    ('BLACK COFFEE PILLOW', 20),
    ('BLACK COFFEE PHONE CASE', 15),
    ('BLACK COFFEE WATER BOTTLE', 20),
    ('BLACK COFFEE NOTEBOOK', 10),
    ('BLACK COFFEE PEN', 5),
    ('BLACK COFFEE PIN', 10),
    ('BLACK COFFEE PATCH', 10),
    ('BLACK COFFEE WALL CLOCK', 30),
    ('BLACK COFFEE PLANT POT', 25),
    ('BLACK COFFEE FRIDGE MAGNET', 5)]

def menu():
    cart = []
    print('Please select one of the options below!\n')
    print('''      
      1 - Add product
      2 - See my products
      3 - Remove product
      4 - Finish and pay
      5 - Exit''')
    while True:
        choice = input('\n----------> ')

        if choice == '1':

            print('Heres the List of our Products:\n')

            for i, (name, price) in enumerate(product_list):
                print(f'{i+1} - {name} ($ {price:.2f})')

            try:
                product = int(input('\nType the number of the product here ---> ')) - 1

            except ValueError:
                print('Please type a valid number!')
                continue

            if 0 <= product < len(product_list):

                selected_name, selected_price = product_list[product]

                qnt_product = int(input('Type the quantity of the product here ---> '))

                total_price = selected_price * qnt_product

                cart.append((selected_name, total_price))

                print(f'''
Thank you!
You added {selected_name} for $ {total_price:.2f}!

What else do you want to do?
''')       
        elif choice == '2':
            if not cart: print('Your cart is empty at the moment. What you want to do?')
            else: 
                total_cart = 0
                print('\nYour cart in the moment has: \n')
                for i, (name, price) in enumerate(cart):
                    print(f'{i+1} - {name} ($ {price:.2f})')
                    total_cart += price
                print(f'\nTotal: $ {total_cart:.2f}\n')
                print('What else do you want to do?')

        elif choice == '3':
            print('Please choose the product you want to remove.\n')
            for i, (product, price_product) in enumerate(cart): print(f'{i+1} - {product} ($ {price_product:.2f})')
            try:
                index = int(input('\nType the number of the product you want to remove ---> ')) - 1
                if 0 <= index < len(cart):
                    removed_product = cart.pop(index)
                    print(f'''\nYou removed {removed_product[0]} from your cart. 

What else do you want to do?''')
            except ValueError: print('Invalid product number! Try again!')    

        elif choice == '4':
            print('Proceeding to payment...')
            payment(cart)
        
        elif choice == '5':
            print('Good bye, and thanks for testing!')
            break
        
        else:
            print('Invalid option, try again!') 

def payment(cart):
    cart
    total = 0
    full_shopping = 0
    discount = 0

    if total >= 400:
        discount = total * 0.15
        print('Congratulations! You got a 15% discount with your shopping list and a Free Sticker Pack!')

    elif total >= 200:
        discount = total * 0.10
        print('Congratulations! You got a 10% discount with your shopping list!')

    print('\nYour cart in the moment has: \n')
    for product, price_product in cart:
        print(f'- {product} ($ {price_product:.2f})')
        total += price_product
    print(f' Your total at the moment is $ {total:.2f}')
    print('''\nHow do you want to pay?

1 - Debit Card
2 - Credit Card
3 - Cash
4 - Back to menu''')
    
    pmnt_choice = input('\n----------> ')

    if pmnt_choice == '1':
        full_shopping = total - discount
        print('You chose to pay with Debit Card. Please wait while we process your payment...') 
        print('\n')
        print('\n')        
    
    elif pmnt_choice == '2':
        tax = total * 0.05
        full_shopping = total + tax - discount
        print('You chose to pay with Credit Card. Credit Card Payments have a 5% tax! Please wait while we process your payment...') 
        print('\n')
        print('\n')       

    elif pmnt_choice == '3':
        cash_discount = total * 0.05
        full_shopping = total - cash_discount
        print('You chose to pay with Cash. You gained a 5% discount! Please wait while we process your payment...') 
        print('\n')
        print('\n')
        

    elif pmnt_choice == '4':
        print('Returning to menu...')
        return

    else: 
        print('Invalid payment option! Please Try again!')

    print(f'Your total is $ {full_shopping:.2f} after discounts and taxes!')
    agreement = input('Do you want to proceed with the payment? (y/n) ---> ')
    if agreement in ['y', 'n']:
        if agreement == 'y':
            print('Payment successful! Thank you for shopping with us!')
            breakpoint()
            
        else:
            print('Payment cancelled. Returning to menu...')
    else:
        print('Invalid option! Please type "y" for yes or "n" for no.')

menu()






