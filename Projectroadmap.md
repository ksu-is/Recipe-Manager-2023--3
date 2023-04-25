conn.execute('''CREATE TABLE IF NOT EXISTS recipes
             (ID INTEGER PRIMARY KEY AUTOINCREMENT,
             NAME TEXT NOT NULL,
             INGREDIENTS TEXT NOT NULL,
             INSTRUCTIONS TEXT NOT NULL,
             COOK_TIME INTEGER NOT NULL,
             DIFFICULTY TEXT NOT NULL);''')

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


def search_recipe():
    search_term = input("Enter search term: ")
    query = f"SELECT * FROM recipes WHERE NAME LIKE '%{search_term}%' \
             OR INGREDIENTS LIKE '%{search_term}%' \
             OR INSTRUCTIONS LIKE '%{search_term}%' \
             OR DIFFICULTY LIKE '%{search_term}%'"
    result = conn.execute(query)
    rows = result.fetchall()
    if len(rows) == 0:
        print("No recipes found.")
    else:
        for row in rows:
                    print("ID:", row[0])
            print("Name:", row[1])
            print("Ingredients:", row[2])
            print("Instructions:", row[3])
            print("Cook Time:", row[4], "minutes")
            print("Difficulty:", row[5])
            print("")
def modify_recipe():
    recipe_id = int(input("Enter recipe ID: "))
    query = f"SELECT * FROM recipes WHERE ID = {recipe_id}"
    result = conn.execute(query)
    rows = result.fetchall()
    if len(rows) == 0:
