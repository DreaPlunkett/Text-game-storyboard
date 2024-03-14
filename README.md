# Text-game-storyboard
IT 140 Design Document 
5-3 Proect 1 
# TextBasedGame.py
# Andrea Jackson
# Print Game Storyboard
def instructions():
    print("\nWelcome to The Magic Adventure Game!,\n", "-----------------------------------", "\n",
          "Lost in the woods, far from home,  you spot a cottage that looks warm and inviting.", "\n",
          "You knock and the door opens slowly but no one replies when you call out.", "\n",
          "As you enter into the entry way the door suddenly closes behind you and you cannot escape.", "\n",
          "Suddenly, your fear spikes sensing a presence within the house.", "\n",
          "Out of nowhere a face appears floating in a ring of fire before you of an old women laughing", "\n",
          "saying that you will never leave this place. And at that moment you realize you must find an exit.", "\n",
          "All magic items must be obtained in order to survive and leave this spelled cottage.", "\n",
          "Good luck and may your internal compass guide you.", "\n",
          "----------------------------------------------------------------------------------------------", "\n",
          "*Instructions*", "\n",
          "Your task is to Collect 6 items to defeat the Evil Sorceress and escape or be trapped forever .\n",
          "To Move, type commands: go South, go North, go East, go West\n",
          "To Add an item to your Magic Inventory, type: get 'magic item nam' ", "\n",
          "You are in the Entry Hall - Let the game begin", "\n",
          "-----------------------------------------------------------------------------------------------", "\n")


instructions()

inventory = []
current_room = "Entry Hall"
# define room and items
items = {
    "Bedroom": "Wand",
    "Kitchen": "Mushroom",
    "Library": "Spellbook",
    "Dining Room": "Armor",
    "Living Room": "Potion",
    "Basement": "",
    "Gallery of Art and Mirrors": "Amulet",
    "Entry Hall": ""
}

rooms = {
    "Entry Hall": {"North": "Kitchen", "South": "Living Room", "East": "Gallery of Art and Mirrors",
                   "West": "Bedroom"},
    "Kitchen": {"South": "Entry Hall", "East": "Dining Room"},
    "Dining Room": {"West": "Kitchen"},
    "Living Room": {"North": "Entry Hall", "East": "Library"},
    "Bedroom": {"East": "Entry Hall"},
    "Gallery of Art and Mirrors": {"West": "Entry Hall", "North": "Basement"},
    "Basement": {"South": "Gallery of Art and Mirrors"},
    "Library": {"West": "Living Room"}
}

while True:
    if len(inventory) < 6 and rooms[current_room] != "Basement":
        print("Magic Inventory:", inventory)
        print("_______________________________________\n")
    move = input("Enter your move:").strip()

    # calling player status function

    if move.startswith("go"):
        direction = move.split()[1].title()
        if direction in rooms[current_room]:
            current_room = rooms[current_room][direction]
            print(f"You are in the {current_room}")
            if items[current_room] and items[current_room] not in inventory:
                print(f"You see a {items[current_room]}")
        else:
            print("Dead end try another direction")

    if current_room == 'Basement':
        print("You must to contend with the Evil Sorceress!")
        if rooms[current_room] == 'Basement':
            print(f"You are in the {current_room}")
        if len(inventory) == 6:
            print("Woohoo!, you have accumulated all magic items. You Win! You are free!", "\n",
                  "CONGRATULATIONS and thank you for playing 'The Magic Adventure Game'")
            break
        else:
            print("Goodness gracious,You have been forced to contend with the Evil Sorceress!")
            print("Magic Inventory :", inventory)
            print("You did not collect all the required magic items and have been killed.", "\n",
                  "Thank you for playing - have fun being stuck forever in the spelled cottage.")
            break

    if move.startswith("get"):
        item = move.split()[1].title()
        if items[current_room] == item:
            inventory.append(item)
            print(f"{item} retrieved !")
        else:
            print(f"Cannot get {items}!")

