---
title: trell-search
date: 2018-04-24 11:46:52
tags:
  - trell
categories:
  - tools

---



## Special Operators

- [Searching for Cards (All Boards) - Trello Help](https://help.trello.com/article/808-searching-for-cards-all-boards)

Search operators refine your search to help you find specific cards and create highly tailored lists. Trello will suggest operators for you as you type, but here’s a full list to keep in mind. 

These operators will also work in the "Archive" search bar. See  [Archiving and deleting cards](https://help.trello.com/article/795-archiving-and-deleting-cards) for more details.

**-operator** - You can add “-” to any operator to do a negative search, such as -has:members to search for cards without any members assigned.

**@name** - Returns cards assigned to a member. If you start typing @, Trello will suggest members for you. **member:** also works. @me will include only your cards.
**label:** - Returns labeled cards. Trello will suggest labels for you if you start typing a name or color. For example, label:"FIX IT" will return cards with the label named “FIX IT”. **#label** also works.

**board:id** - Returns cards within a specific board. If you start typing board:, Trello will suggest boards for you. You can search by board name, too, such as “board:trello” to search only cards on boards with trello in the board name.

```

-board:parkbox spring // search spring except board parkbox
```



**list:name** - Returns cards within the list named “name”. Or whatever you type besides “name”.

**has:attachments** - Returns cards with attachments. **has:description**, **has:cover**, **has:members**, and **has:stickers** also work as you would expect.

**due:day** - Returns cards due within 24 hours. **due:week** returns cards that are due within the following 7 days. **due:month**, and **due:overdue** also work as expected. You can search for a specific day range. For example, adding due:14 to search will include cards due in the next 14 days. You can also search for **due:complete** or **due:incomplete** to search for due dates that are marked as complete or incomplete.

**created:day** - Returns cards created in the last 24 hours. **created:week** and **created:month** also work as expected. You can search for a specific day range. For example, adding created:14 to the search will include cards created in the last 14 days.

**edited:day** - Returns cards edited in the last 24 hours. **edited:week** and **edited:month** also work as expected. You can search for a specific day range. For example, adding edited:21 to the search will include cards edited in the last 21 days.

**description:**, **checklist:**, **comment:**, and **name:** - Returns cards matching the text of card descriptions, checklists, comments, or names. For example, comment:"FIX IT" will return cards with “FIX IT” in a comment.

**is:open** returns open cards. **is: archived** returns archived cards. If neither is specified, Trello will return both types.

**is:starred** - Only include cards on starred boards.