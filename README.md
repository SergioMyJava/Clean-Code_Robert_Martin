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
 10. [Classes](#classes)
 11. [Systems](#systems)
 12. [Emergence](#emergence)
 13. [Concurrency](#concurrency)
 14. [Smells and Heuristics](#smells-and-heuristics)
  
  
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
  
  The number of assert directives in the test should be minimized.
  
  Five characteristics for good tests:
* Tests must be performed quickly.
* Tests should not depend on each other.
* Tests should give repeatable results in any environment.
* The result of the test should be a logical sign. The test either passed or did not pass.
* Tests should be created in a timely manner.

  For the "health" of the project tests are no less important than the product code. Or maybe they are even more 
  important because the tests retain and improve the flexibility, maintainability and reusability of the product code.
  
  ## **Classes**
  
  The list of variables is usually followed by open functions.
  
  Classes should be compact.
  
  If the class fails to pick a clear one, the short name is probably too large.
  
  The principle of common responsibility (SRP1) states that a class or module must have one - and only one - reason for 
  the change.
  
  Try to separate the variables and methods into two or more classes so that the new classes have higher connectivity.
  
  ## **Systems**
  
  The concept of sharing responsibility is one of the oldest and most important techniques.
  
  In software systems, the initialization phase, in which the application objects are constructed and the main 
  dependencies “stick together”, must also be separated from the runtime logic, which receives control after its 
  completion.
  
  This is the most important difference between software systems and physical ones. The architecture of software systems 
  can be developed consistently, if we ensure the correct division of responsibility.
  
  Finally, the most comprehensive tool for separating areas of responsibility through the use of aspects is AspectJ1, 
  a Java extension that provides “full-fledged” support for aspects like modular designs. There are enough pure Java 
  solutions based on Spring and JBoss for 80–90% of situations in which aspects are applied.
  
  If you can write the domain logic of your application in the form of POJO-objects separated from any architectural 
  areas of responsibility at the code level, then you will have the opportunity to conduct full-fledged tests of your 
  architecture.
  
  The optimal system architecture consists of modular areas of responsibility, each of which is implemented on the basis 
  of POJO objects. Areas are integrated with each other through aspects or similar means that minimally interfere with 
  their work. Such architecture can be built on the basis of development methodology through testing, as well as program 
  code.
  
  As you know, it is best to entrust responsible decisions to the most qualified. However, we often forget that 
  decision-making is best postponed until the last moment (at the moment when all the information is known, or almost 
  all of the problems that may arise on the project).
  
  The flexibility of a POJO system with modular areas of responsibility allows you to make optimal, timely decisions 
  based on the latest information. In addition, it helps reduce the complexity of such solutions.
  
  Standards simplify the reuse of ideas and components, attracting people with the necessary experience, translating 
  successful ideas and linking components. However, the process of creating a standard sometimes takes too much time 
  (and the industry does not stand still), with the result that standards lose touch with the real needs of the people 
  they should serve.
  
  Subject-oriented languages allow you to express in the form of POJO-objects all levels of abstraction and all 
  application domains, from high-level policies to low-level technical details.
  
  Clean should be not only the code, but also the system architecture.
  
  Regardless of whether you are designing a whole system or its individual modules, remember: use the simplest solution 
  possible.
  
  ## **Emergence**
  
  According to Kent, an architecture can be considered “simple” if it:
  * ensures that all tests pass (The system, thoroughly tested and passed all tests, is controlled.)
  * does not contain duplicate code
  * expresses the intentions of the programmer,
  * uses the minimum number of classes and methods.
  The rules are listed in order of importance.
  
  Our goal is to make the system compact, but at the same time preserve the compactness of functions and classes. 
  However, it should be remembered that of the four simple architecture rules, this rule has the lowest priority. 
  Minimizing the number of functions and classes is important, but passing tests, eliminating duplicates and expressive 
  code is still more important.
  
  ## **Concurrency**
  
  A multitude of common myths and misconceptions are associated with multithreading:
  
  * Multithreading always improves performance.
  Multithreading improves performance, but only with a relatively large wait time, which could be effectively used by 
  other threads or processors.
  
  * Writing a multi-threaded code does not change the architecture of the program.
  The architecture of a multithreaded algorithm may differ significantly from the architecture of a single-threaded 
  system. Separating the “what” from the “when” usually has a huge impact on the structure of the system.
  
  * When working with a container (for example, a web container or an EJB container) it is not necessary to understand 
  the problems of multi-threaded programming.
  It is advisable to know how the container works and how to protect against problems of simultaneous updating and 
  deadlocks.
  
  Some more objective statements related to writing multi-threaded code:
  
  * Multithreading is associated with certain additional costs - both in terms of productivity, and writing additional 
    code.
  * Proper implementation of multithreading is difficult even for simple tasks.
  * Errors in multi-threaded code are usually not reproduced, therefore they are often ignored as random deviations1 
    (and not as systematic defects that they really are).
  * Multithreading often requires fundamental changes in the design strategy.
  
  Separate code related to multithreading implementation from the rest of the code.Corollary: limit the area data 
  visibility.
  
  Be serious about data encapsulation; severely restrict access to all shared data.

  Streams should be as independent as possible.
  
  Logical partitioning patterns of program behavior.
  
         1. Сonsumer model makers.
            One or more producer threads create jobs and put them in a buffer or queue. One or more consumer threads 
            retrieve jobs from the queue and execute them
  
         2. Model "readers-writers"
            The designer must find a balance between the needs of readers and writers to ensure the correct mode of 
            operation, normal system performance and avoid lag.
            
         3. Model "dining philosophers problem"
            Applications compete for resources from a limited set. If you carelessly design such a system, then the 
            competition between threads can lead to interlocks, reversible locks, and a drop in productivity and work 
            efficiency. 
            
  Beware of dependencies between synchronized methods. If the generic class contains more than one synchronized method, 
  your system may not be designed correctly.
  
  Synchronized sections must have a minimum size. The code should contain as few synchronized sections as possible.
  
  Testing does not guarantee the correct operation of the code. However, quality testing minimizes risk.
  
  Treat non-periodic failures as signs of potential multithreading problems.
  
  Start by debugging non-threaded core code.
  
  Implement your multithreaded code so that it can be executed in various configurations.
  
  Provide logical isolation for multi-threaded code configurations.
  
  Test the program with the number of threads in excess of the number of processors.
  
  Test the program on different platforms.
  
  ## **Smells and Heuristics**
  
     ### Comments

        It is inappropriate to post information in comments that is more convenient to store in other sources: in source 
        control systems, in version control systems and in other logging systems.  
        
        A comment whose contents have lost relevance is considered obsolete.
        
        Excess is considered to be a comment describing something that is already obvious.
        
        Choose your words carefully. Keep track of spelling and punctuation. Do not write messy. Do not explain the 
        obvious. Be concise.
        
        After seeing the commented out code, delete it! Do not worry, the source control system will not forget it.
  
     ### Workspace
     
        Building a project should be one trivial operation. Without sampling numerous fragments from source control. 
        Without a long series of unintelligible commands or context-sensitive scripts to build individual elements. 
        Without searching for additional files in the format of JAR, XML and other artifacts necessary for your system.
        
        All unit tests should be performed with just one command. worst case one simple command is entered on the 
        command line.
        
     ### Functions
     
        Functions should have a small number of arguments. Best of all, when there are no arguments at all; functions 
        with one, two, and three arguments follow.   
        
        Output arguments are unnatural.
        
        Eliminate logical arguments from functions.
        
        If the method is never called in the program, then it should be deleted.
        
     ### Different
     
        Ideally, the source file should contain code in the same language.at the very least, both the amount and amount 
        of code in additional languages in the source files should be minimized.  
        
        Any function or class must implement the behavior that the programmer can expect from them. 
        
        Disabling security is risky.
        
        Avoid duplication.
        
        All low-level concepts should be concentrated in derived classes, and all high-level concepts are combined in 
        the base class.
        
        In general, base classes should not know anything about their derived classes.
        
        Placing the derived and base classes in different jar files, in which the base jar files do not know anything 
        about the contents of the derived jar files, allows you to organize the deployment of systems in the format of 
        discrete, independent components.
        
        Good developers know how to limit the interfaces of their classes and modules. The less methods a class 
        contains, the better. The fewer variables a function is known, the better. The fewer instance variables the 
        class contains, the better.
        
        Do not regret time - figure out where the declaration of a particular function, constant or variable should be 
        located.
        
        In general, give preference to non-static methods over static ones.
        
        If one module depends on another, the dependence must be not only logical, but also physical.
        
        Before using switch, consider using polymorphism.
        
        All function commands must be formulated at the same level of abstraction, which is located one level below the 
        operation described by the function name.
        
        If A interacts with B, and B interacts with C, then modules using A should not be aware of C.
        
        If you use two or more classes from a package, import the entire package.
        
        For each type of choice, the program must not contain more than one switch command. Multiple switch 
        constructions should be replaced with polymorphic objects.
        
        Functions must perform one operation.
        
        The time reference is implemented by creating a “relay race”.
        
        Encapsulate boundary conditions
        
        Make sure the names are meaningful.
        
       Names must reflect the level of abstraction at which the class or function operates.
       
       Names are easier to understand if they are based on existing conventions or standard notation.
        
       The length of the name must match the length of its scope.
       
       Names should describe everything that a function, variable, or class does.
       
       The test package should test everything that might break.
       
       Mistakes are often collected in groups.
       
       Do everything you need to make your tests run fast.
       
        