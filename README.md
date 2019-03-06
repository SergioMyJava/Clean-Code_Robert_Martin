Clean Code. Robert Martin
===========================

 1. [Clean Code](#clean-code)
 2. [Meaningful Names](#meaningful-names)
 3. [Functions](#Functions)
 4. [Comments](#Comments)
 5. [Formatting]()
 6. [Objects and Data Structures]()
 7. [Error Handling]()
 8. [Boundaries]()
 9. [Unit Tests]()
 10. [Classes]()
 11. [Systems]()
 12. [Emergence]()
 13. [Concurrency]()
 14. [Successive Refinement]()
 15. [JUnit Internals]()
 16. [Refactoring SerialDate]()
 17. [Smells and Heuristics]()
  
  
  ## Clean Code
  
  If you have been programming for more than two or three years, you probably have been bogged down in someone 
  else’s - or in your own - erratic course. Slowing can be quite significant. For some year or two groups, very quickly
  moving forward at the very beginning of the project, they begin to crawl at the speed of the cochlea. Each change to 
  the code breaks the code in two or three places. No change is trivial. For each addition or modification of the 
  system, it is necessary to “understand” all the intricacies of the code - so that in the program they become even 
  more. Over time, the confusion grows so much that it is no longer possible to cope with it. You just do not move.
  
  To write a clean code, you must consciously apply a variety of techniques, guided by a sense of "purity" acquired by 
  hard work. A key role here is played by the “code sense”. Some are born with this feeling. Others work to develop it. 
  This feeling not only makes it possible to distinguish good code from bad code, but also demonstrates the strategy of 
  using our skills to transform bad code into clean code.
  
  In short, a clean code programmer is an artist who navigates a blank screen through a series of transformations until 
  he becomes an elegantly programmed system.
  
  
  ## **Meaningful Names**
  
  Watch the names in your programs and change them if you find more successful options. This will simplify the life of 
  everyone who reads your code (including yourself).
  
  **Bad:**
  ```java
  public List<int[]> getThem() {
  List<int[]> list1 = new ArrayList<int[]>();
  for (int[] x : theList)
  if (x[0] == 4)
  list1.add(x);
  return list1;
  }
  ```
  
  **Good:**
  ```java
  public List<Cell> getFlaggedCells() {
  List<Cell> flaggedCells = new ArrayList<Cell>();
  for (Cell cell : gameBoard)
  if (cell.isFlagged())
  flaggedCells.add(cell);
  return flaggedCells;
  }
  ```
  
  Programmers should avoid false associations that obscure the meaning of the code. Do not use words with hidden 
  meanings other than intended.
  
  If the names are different, then they must denote different concepts.
  
  Names should be pronounced normally.
  
  Single-letter names can ONLY be used for local variables in short methods.
  
  We already have enough trouble with coding to look for new difficulties. Encoding information about the type or scope 
  in names only creates new decryption efforts.
  
  Do not force the reader to mentally convert your names to others already known to him.
  
  The names of classes and objects must be nouns and their combinations.
  
  Method names are verbs or verb phrases.
  
  Names should be placed in a specific context for the reader of the code, enclosing them in classes, functions, and 
  namespaces with well-chosen names.
  **Bad:**
  ```java
  private void printGuessStatistics(char candidate, int count) {
  String number;
  String verb;
  String pluralModifier;
  if (count == 0) {
  number = "no";
  verb = "are";
  pluralModifier = "s";
  } else if (count == 1) {
  number = "1";
  verb = "is";
  pluralModifier = "";
  } else {
  number = Integer.toString(count);
  verb = "are";
  pluralModifier = "s";
  }
  String guessMessage = String.format(
  "There %s %s %s%s", verb, number, candidate, pluralModifier
  );
  print(guessMessage);
  }
  ```
  
  **Good:**
  ```java
  public class GuessStatisticsMessage {
  private String number;
  private String verb;
  private String pluralModifier;
  public String make(char candidate, int count) {
  createPluralDependentMessageParts(count);
  return String.format(
  "There %s %s %s%s",
  verb, number, candidate, pluralModifier );
  }
  private void createPluralDependentMessageParts(int count) {
  if (count == 0) {
  thereAreNoLetters();
  } else if (count == 1) {
  thereIsOneLetter();
  } else {
  thereAreManyLetters(count);
  }
  }
  private void thereAreManyLetters(int count) {
  number = Integer.toString(count);
  verb = "are";
  pluralModifier = "s";
  }
  private void thereIsOneLetter() {
      number = "1";
      verb = "is";
      pluralModifier = "";
      }
      private void thereAreNoLetters() {
      number = "no";
      verb = "are";
      pluralModifier = "s";
      }
  }
  ```
  
  ## **Functions**
  
  The first rule: functions must be compact. The second rule: functions should be even more compact.
  HE FUNCTION MUST BE PERFORMED ONLY ONE OPERATION. SHE MUST BE FULFILLED BY IT. AND ANYTHING OTHER SHE MUST NOT DO.
  
  To make sure that the function performs “only one operation,” you need to check that all the function commands are at 
  the same level abstraction.
  
  A long meaningful name is better than a short unintelligible.
  
  In the ideal case, the number of function arguments is zero (a zero-ary function). The following are functions with 
  one argument (unary) and two arguments (binary). Functions with three arguments (ternary) should be avoided whenever 
  possible.
  
  A function must do something or answer a question, but not at the same time.
  
  For this reason, the bodies of try and catch blocks are recommended to be allocated to separate functions.
  
  **Good:**
  ```java
  public void delete(Page page) {
  try {
  deletePageAndAllReferences(page);
  }
  catch (Exception e) {
  logError(e);
  }
  }
  private void deletePageAndAllReferences(Page page) throws Exception {
  deletePage(page);
  registry.deleteReference(page.name);
  configKeys.deleteKey(page.name.makeKey());
  }
  private void logError(Exception e) {
  logger.log(e.getMessage());
  }
  ```
  
  ## **Comments**