Open fennec with url via Intent:

```java
private void goFF(String url) {
        String FFurl = ((url!= null) && !url.equalsIgnoreCase("")) ? url : "http://manichord.com/";
        Intent intent = new Intent(Intent.ACTION_MAIN, null);
        intent.addCategory(Intent.CATEGORY_DEFAULT);
        intent.addCategory(Intent.CATEGORY_BROWSABLE);
        intent.setComponent(new ComponentName("org.mozilla.firefox_beta", "org.mozilla.firefox_beta.App"));
        intent.setAction(Intent.ACTION_VIEW);
        intent.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
        intent.setData(Uri.parse(FFurl));
        startActivity(intent);
    }
```