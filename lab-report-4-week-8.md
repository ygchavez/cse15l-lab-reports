# Lab Report 4

[My markdown-parse Repository](https://github.com/ygchavez/markdown-parse)


[Reviewed markdown-parse Repository](https://github.com/Alexander-Kourjanski/markdown-parse)

## Snippet 1
### Should Produce : 
```
[`google.com, google.com, ucsd.edu]
```
### My Test Code:
```
    @Test
    public void testSnippet1() throws IOException {
        String regFile = Files.readString(Path.of("./snippet-1.md"));
        String[] regLines = regFile.split("\n");
        assertEquals(List.of("`google.com", "google.com", "ucsd.edu"), MarkdownParse.getLinks(regLines));
    }
```
### Reviewer Test Code:
```
    @Test
    public void testSnippet1() throws IOException {
        ArrayList<String> testfile2 = new ArrayList<>();
        testfile2.add("`google.com");
        testfile2.add("google.com");
        testfile2.add("ucsd.edu");
        String testfilemd = MarkdownParse.converter("./snippet-1.md");
        assertEquals(testfile2, MarkdownParse.getLinks(testfilemd));
    }
```
### My Output:
```
1) testSnippet1(MarkdownParseTest)
java.lang.AssertionError: expected:<[`google.com, google.com, ucsd.edu]> but was:<[url.com, `google.com, google.com, ucsd.edu]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.testSnippet1(MarkdownParseTest.java:36)
```
### Reviewed Output:
```
1) testSnippet1(MarkdownParseTest)
java.lang.AssertionError: expected:<[`google.com, google.com, ucsd.edu]> but was:<[url.com, `google.com, google.com]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.testSnippet1(MarkdownParseTest.java:87)
```
__Do you think there is a small (<10 lines) code change that will make your program work for snippet 1 and all related cases that use inline code with backticks? If yes, describe the code change. If not, describe why it would be a more involved change.__

Yes I do think there is a small code change that will make my program work for this snippet and all related cases. To do this I will add code to check for brackets and make sure that there’s a space in between the outer bracket and the inner parenthesis since it is currenlty able to process the backticks but needs to check for valid links.

## Snippet 2
### Should produce:
```
[a.com, a.com(()), example.com]
```
### My Test Code:
```
    @Test
    public void testSnippet2() throws IOException {
        String regFile = Files.readString(Path.of("./snippet-2.md"));
        String[] regLines = regFile.split("\n");
        assertEquals(List.of("a.com", "a.com(())", 
            "example.com"), MarkdownParse.getLinks(regLines));
    }
```
### Reviewer Test Code:
```
    @Test
    public void testSnippet2() throws IOException {
        ArrayList<String> testfile2 = new ArrayList<>();
        testfile2.add("a.com");
        testfile2.add("a.com(())");
        testfile2.add("example.com");
        String testfilemd = MarkdownParse.converter("./snippet-2.md");
        assertEquals(testfile2, MarkdownParse.getLinks(testfilemd));
    }
```
### My Output:
```
2) testSnippet2(MarkdownParseTest)
java.lang.AssertionError: expected:<[a.com, a.com(()), example.com]> but was:<[a.com, a.com((, example.com]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.testSnippet2(MarkdownParseTest.java:43)
```
### Reviewed Output:
```
2) testSnippet2(MarkdownParseTest)
java.lang.AssertionError: expected:<[a.com, a.com(()), example.com]> but was:<[a.com, a.com((]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.testSnippet2(MarkdownParseTest.java:97)
```
### Answering Question #2:

I think that I can just make a small code change to make my program work for snippet 1 and all related cases. First, I would add a stack/counter algorithm (probably only 8 lines) to get the outer parenthesis and not just stop at the beginning one. Then, my code will work alright. It was already able to process the links correctly, but it just didn't get the other outer parenthesis. 


## Snippet 3