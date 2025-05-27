df['price'] = df['Price'].str.replace('Ksh', '', regex = False).str.replace(',', '', regex = False) # => regex - 

regex - regular expression
- is a sequence of characters that forms a search pattern
- Used to check if a string contains the specified search pattern