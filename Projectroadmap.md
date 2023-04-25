conn.execute('''CREATE TABLE IF NOT EXISTS recipes
             (ID INTEGER PRIMARY KEY AUTOINCREMENT,
             NAME TEXT NOT NULL,
             INGREDIENTS TEXT NOT NULL,
             INSTRUCTIONS TEXT NOT NULL,
             COOK_TIME INTEGER NOT NULL,
             DIFFICULTY TEXT NOT NULL);''')

# Function to add a new recipe
def add_recipe():
    name = input("Enter recipe name: ")
    ingredients = input("Enter ingredients separated by commas: ")
    instructions = input("Enter instructions: ")
    cook_time = int(input("Enter cook time (in minutes): "))
    difficulty = input("Enter difficulty level: ")
    conn.execute(f"INSERT INTO recipes (NAME, INGREDIENTS, INSTRUCTIONS, COOK_TIME, DIFFICULTY) \
                   VALUES ('{name}', '{ingredients}', '{instructions}', {cook_time}, '{difficulty}');")
    conn.commit()
    print("Recipe added successfully!")
