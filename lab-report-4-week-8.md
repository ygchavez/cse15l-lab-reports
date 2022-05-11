# Lab Report 4

[My markdown-parse Repository](https://github.com/ygchavez/markdown-parse)


[Reviewed markdown-parse Repository](https://github.com/Alexander-Kourjanski/markdown-parse)

## Snippet 1
### This should produce: l
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

Yes, I do think there is a small code change that will make my program work for this snippet and all related cases. To do this I will add code to check for brackets and make sure that there’s a space in between the outer bracket and the inner parenthesis since it is currenlty able to process the backticks but needs to check for valid links.

## Snippet 2
### This should produce:
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
__Do you think there is a small (<10 lines) code change that will make your program work for snippet 2 and all related cases that nest parentheses, brackets, and escaped brackets? If yes, describe the code change. If not, describe why it would be a more involved change.__

Yes I do think there is a small code change that will make my program work for this snippet and all related cases. To do this I will add a counter algorithm to not just stop at the beginning one and get the outer parenthesis.

## Snippet 3
### This should produce:
```
[https://www.twitter.com, https://ucsd-cse15l-w22.github.io/, https://cse.ucsd.edu/]
```
### My Test Code:
```
    @Test
    public void testSnippet3() throws IOException {
        String regFile = Files.readString(Path.of("./snippet-3.md"));
        String[] regLines = regFile.split("\n");
        assertEquals(List.of("https://www.twitter.com", "https://ucsd-cse15l-w22.github.io/", 
            "https://cse.ucsd.edu/"), MarkdownParse.getLinks(regLines));
    }
```
### Reviewer Test Code:
```
    @Test
    public void testSnippet3() throws IOException {
        ArrayList<String> testfile2 = new ArrayList<>();
        testfile2.add("https://www.twitter.com");
        testfile2.add("https://ucsd-cse15l-w22.github.io/");
        testfile2.add("https://cse.ucsd.edu/");
        String testfilemd = MarkdownParse.converter("./snippet-3.md");
        assertEquals(testfile2, MarkdownParse.getLinks(testfilemd));
    }
```
### My Output:
```
3) testSnippet3(MarkdownParseTest)
java.lang.AssertionError: expected:<[https://www.twitter.com, https://ucsd-cse15l-w22.github.io/, https://cse.ucsd.edu/]> but was:<[, , ]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.testSnippet3(MarkdownParseTest.java:52)
```
### Reviewed Output:
```
3) testSnippet3(MarkdownParseTest)
java.lang.AssertionError: expected:<[https://www.twitter.com, https://ucsd-cse15l-w22.github.io/, https://cse.ucsd.edu/]> but was:<[
    https://www.twitter.com
,
    https://ucsd-cse15l-w22.github.io/
, github.com

And there's still some more text after that.

[this link doesn't have a closing parenthesis for a while](https://cse.ucsd.edu/



]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.testSnippet3(MarkdownParseTest.java:107)
```
__Do you think there is a small (<10 lines) code change that will make your program work for snippet 3 and all related cases that have newlines in brackets and parentheses? If yes, describe the code change. If not, describe why it would be a more involved change.__

I don't think it is possible for me to make a small code change to make my program work for snippet 3 and all related cases. My program currently splits up each line into it's own quote meaning I would have to restart how it takes in text lines, causing the implementation of more than 10 lines of code.