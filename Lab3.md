## Lab3 Report : Squashing some bugs!
***
Getting more familiar with Java's helper methods is fine and all, but what use are those methods if Java is not told what to do in the correct manner! Remember, computers need specific and definite instructions to do thier job. In that case, what happens when our silly human brains muck it up and make a mistake in out code? Well, we are left with a **bug**!

In our lab section last week, we made use of `Junit` and its methods to go over some given methods and write tests, some of these methods however did not always work when they were tested! This unexpected output is called a `symptom` while the actual error in the code itself is the bug we need to find and squash!

Looking back at the given code, lets look at the `merge` method in our `ListExamples.java` file, here we'll spot a simple bug, but a code-breaking bug nonetheless.
```
 static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index1 += 1;
    }
    return result;
  }
```

Can you see the bug in  the given code? If not thats alright, first lets look at the test that brought the issue to light!

```
public class ListTests {
    
    @Test
    public void testMerge(){
        List<String> lst1 = new ArrayList<>();
        List<String> lst2 = new ArrayList<>();
        List<String> expected = new ArrayList<>();
        List<String> result = new ArrayList<>();

        lst1.add("apple"); lst1.add("clementine"); lst1.add("egg");
        lst2.add("burger"); lst2.add("danishes"); lst2.add("frenchToast");
        expected.add("apple"); expected.add("burger"); expected.add("clementine"); expected.add("danishes"); expected.add("egg"); expected.add("frenchToast");

        result = ListExamples.merge(lst1, lst2);

        assertEquals(expected, result);
    }

}
```

Now, the `merge` function is meant to take two `String` type `ArrayList`s and then combine them into an alphebetically ordered `ArrayList` containing *all* the words in the two inputs, runnign everything as-is, however, we get the following:

