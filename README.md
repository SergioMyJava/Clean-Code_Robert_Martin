Clean Code. Robert Martin
===========================

 1. [Clean Code](#clean-code)
 2. [Meaningful Names](#meaningful-names)
 3. [Functions](#functions)
 4. [Comments](#comments)
 5. [Formatting](#formatting)
 6. [Objects and Data Structures](#objects-and-data-structures)
 7. [Error Handling](#error-handling)
 8. [Boundaries](#boundaries)
 9. [Unit Tests](#unit-tests)
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
  
  Nothing helps in the proper way to comment. Nothing clutters the module as empty and peremptory comments. Nothing does
  so much harm, like an old commentary that has lost relevance, spreading lies and misinformation.
  
  The older the commentary, the farther it is from the code it describes, the greater the likelihood that it is simply 
  incorrect.
  
  Sometimes it is useful to leave notes “for the future” in the form of comments // TODO.
  
  Headlines attract attention only if they are not found too often. Use them sparingly and only when they bring tangible
  benefits.
  
  In programming, rarely habits are more disgusting than commenting off unused code. Never do it!
  
  Do not present system-level information in the context of local commentary.
  
  ## **Formatting**
  
  Code formatting is aimed at information transfer, and information transfer is the primary task of a professional 
  developer.
  
  Almost all the code is read from left to right and from top to bottom. Each line represents an expression or 
  condition, and each group of lines represents a complete thought.
  
  Concepts that are closely related to each other should be vertically close to each other.
  
  Variables should be declared as close as possible to the place of use. In some cases, a variable may be declared at 
  the beginning of a block or immediately before a cycle in a long function.
  
  Some code fragments require that they be placed close to other fragments. Such fragments have a certain conceptual 
  relationship. The stronger the relationship, the less should be the vertical distance between them.
  
  The called function must be located below the calling function.
  
  The source file has a hierarchical structure. File-level commands (such as most class declarations) do not indent. 
  Methods in classes are shifted one level to the right of the class level. Implementations of these methods are shifted
  one level to the right of the class declaration. Block implementations are shifted one level to the right of their 
  outer blocks, and so on.
  
  **Bad**
  ```java
  public class FitNesseServer implements SocketServer { private FitNesseContext
  context; public FitNesseServer(FitNesseContext context) { this.context =
  context; } public void serve(Socket s) { serve(s, 10000); } public void
  serve(Socket s, long requestTimeout) { try { FitNesseExpediter sender = new
  FitNesseExpediter(s, context);
  sender.setRequestParsingTimeLimit(requestTimeout); sender.start(); }
  catch(Exception e) { e.printStackTrace(); } } }
  ```
  
  
   **Good:**
  ```java
  public class FitNesseServer implements SocketServer { 
    private FitNesseContext context;
    public FitNesseServer(FitNesseContext context) {
      this.context = context;
    }
    public void serve(Socket s) {
      serve(s, 10000);
    }
    public void serve(Socket s, long requestTimeout) {
    try {
      FitNesseExpediter sender = new FitNesseExpediter(s, context);
      sender.setRequestParsingTimeLimit(requestTimeout);
      sender.start();
    }
    catch (Exception e) {
      e.printStackTrace();
    }
  }
}
```

  The code of the software product must be issued in the same style.It should not look like it was written by several 
  personalities who disagree about the design. In no case do not complicate the source code, allowing its design in 
  several different styles.
  
  ## **Objects and Data Structures**
  
  To find the best way to present the data contained in an object, you need to seriously consider. Thoughtless addition 
  of reading and writing methods is the worst possible option.
  
  Objects hide their data behind abstractions and provide functions that work with this data. Data structures disclose 
  their data and have no meaningful functions.
  
  Procedural code (code using data structures) makes it easy to add new functions without changing existing data 
  structures. Object-oriented code, on the other hand, makes it easy to add new classes without changing existing 
  functions.
  
  Class C method f should be limited to calling methods of the following objects:
   * C;
   * objects created by f;
   * objects passed to f as argument;
   * objects stored in instance variable C.
   
  Objects provide behavior and hide data. This allows the programmer to easily add new kinds of objects without changing
  the existing behavior. On the other hand, objects make it difficult to add new behavior to existing objects. Data 
  structures provide data, but do not have any significant behavior. They simplify the addition of new behavior to 
  existing data structures, but make it difficult to add new data structures to existing functions.
  
  ## **Error Handling**
  
  Writing code that can trigger exceptions is recommended to start with try-catch-finally.
  
  Use unverifiable exceptions.There are no checked exceptions in C #, and despite all the gallant attempts, they never 
  appeared in C ++. They are also not in Python and Ruby.However, reliable programs can be written in all these 
  languages. The price of checked exceptions is a violation of the principle of openness / closeness.
  
  Each exception that is raised in a program must contain enough contextual information to determine the source and 
  location of the error.
  
  By returning null, we are actually creating extra work for ourselves, and unnecessary problems for the caller. It is 
  worth skipping just one null check, and the application “goes into a corkscrew”.
  
  If you want to return null from a method, consider issuing an exception or returning an “special case” object.
  
  Returning null from methods is bad, but it is even worse to pass null when called.
  
  In most programming languages, there is no good way to handle the random transfer of null from the caller. And if so,
  it is reasonable to prohibit the transmission of null by default.
   
  ## **Boundaries**
  
  We recommend limiting the transmission of the Map (or any other boundary interface) on the system. If you use a 
  interface like Map, keep it inside a class (or a closely related family of classes) in which it is used.
  
  To ensure that borders with third-party code do not create problems in our projects, we minimize the number of calls 
  to them. To do this, you can use wrappers, as in the Map example, or implement the ADAPTER pattern to match our ideal 
  interface with the real one received from the developers.
  
  ## **Unit Tests**
  
  The first law. Do not write the product code until you write a failing unit test.
  The second law. Do not write a unit test in a volume larger than necessary for failure. The impossibility of compiling
  is a failure.
  The third law. Do not write the product code in the amount larger than necessary to pass the current failing test.
  
  Tests "in haste" are equivalent to the complete absence of tests, if not worse. The fact is that tests should change 
  as the product code develops. The more primitive the tests, the harder it is to change them. If the test code is 
  heavily entangled, it may be that writing a new product code will take less time than trying to cram new tests into 
  an updated package.
  
  The test code is as important as the product code.
  
  If you do not maintain the purity of your tests, then you lose them. And without tests, all that provides the 
  flexibility of the product code is lost.
  
  Readability in unit tests is even more important than in the product code.
  
  Much of what you will never do in a product exploitation environment looks absolutely normal in a testing environment. 
  Usually we are talking about the cost of memory or the efficiency of the processor - but never about the problems of 
  cleanliness of the code.