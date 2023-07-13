# Poke API Graphql team builder UI

---

## Introduction

Based on the pokeapi I want to implement a basic team builder for the trainers to be able to register their desired Pokémon teams

### Official api doc

[https://pokeapi.co/docs/graphql](https://pokeapi.co/docs/graphql)

## Requirements

- [ ]  User should be able to choose the trainer avatar alongside a nickname
- [ ]  User should be able to select a maximum of 6 Pokémon peer team builded
- [ ]  Every Pokémon should know at least one move
- [ ]  Every Pokémon can handle an item
- [ ]  The information should be saved for future use
- [ ]  The user can name their teams
- [ ]  The teams can be deleted

### Non-goals

- [ ]  Pagination to avoid performance issues
- [ ]  The search section of every kind of thing should be able to persist the last query
- [ ]  Should be implemented with unit tests to avoid issues
- [ ]  The trainer can choose any Pokémon created officially at the moment

## System overview

![Poke API overview.drawio.png](Poke%20API%20Graphql%20team%20builder%20UI%209bd475e2897e4839a64689899d2d8fb5/Poke_API_overview.drawio.png)

1. React: Bullet prof technology to handle the front end and create a well UI
2. Apollo client: To consume the api due to the good memory system alongside the benefits of use hooks
3. Local storage: as persistence strategy for this version 1
4. Poke API as data source and backend created with GraphQL to fetch the Pokémon information and the images

## Solution

### Avatar selection (profile section for header or nab at)

- Create the GraphQL query to fetch all the available avatars
- Fetch the avatars when the user goes to the user selection
- Add loading animation while fetching the avatars
- Create avatar grid component to display the results
- Implement an input for the nickname
- Implement save / cancel buttons for the profile creation / edit

### Team building main page

- Create team main page
- Create teams list component
- Implement input for team name
- Create delete button to delete team
- Create create button component to redirect to the /team/create page
- Create edit button to redirect the user to the /team/Id/edit
- Create see button to see the team details

### Team building create / edit page

- Create button to add Pokémon to the team
- Create input with default value the index of the team
- render in an horizontal way the pokemon list
- Create modal to setup the Pokémon information
- Create option to remove the Pokémon from the team

### Team building add/update Pokémon

- Create modal component
- Create query to fetch Pokémon list as lazy query
- Display Pokémon list with the name and basic stats
- Display the selected Pokémon in a card or display empty card to be filled as the user setup the Pokémon
- Add a section to select the item and display the list as tab option hiding the Pokémon list using pagination system too
- Implement search input to search the desired Pokémon
- Implement search input to search the desired item to equip to the Pokémon
- Implement add and cancel buttons for the modal to add or update the Pokémon settings

### Pokémon move set

- Create query to fetch the move set list that belongs to the selected Pokémon
- Validate first if the user has already chosen a Pokémon to fetch the novelist, otherwise display message to tell the user to choose one Pokémon
- Display the 4 maximum allowed moves in a square

### Persist user changes

- After every change made and clicked on any save option persist the information
- Create strategy to load in memory the information persisted in local storage
- Create context api to save in memory all the information
- Try to use redux like strategy
- Desired data structure:

```tsx
interface IItem {
	id: string;
	name: string;
	img: string;
}

interface IMovement {
	id: string;
	name: string;
	category: string;
}

interface IPoke {
	id: string;
	name: string;
	item: IItem;
	movements: IMovement[];
	stats: Record<string, number>[]; // neutral nature ones
}

interface ITeam {
	id: string;
	name: string;
	members: IPoke[];
}

interface ITrainerDataStorage {
	nickname: string;
	avatarUrl: string;
	teams: ITeam[];
}
```

## Considerations

### Concerns

Will be enough the api information to fulfill the requirements?

How will affect the performance the persistence strategy of use the local storage?

Will be able to mock the data for the needed scenarios?

## Metrics

Try to achieve a MVP

Try to reach at least a 90% of coverage