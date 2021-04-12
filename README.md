
# Rapport WebView
En applikation skapades med webview element för att kunna inkorporera hemsidor inuti applikationen.

1.  Update app name
Uppdaterade applikationens namn genom values --> strings.xml under string name, till MyWebViewApp
från WebViewApp. Denna förändring uppvisades i toppbaren där applikationsnamnet visades.
(Se bild i steg 6, 7, och 8).
```
<resources>
    <string name="app_name">MyWebViewApp</string>
    ...
</resources>
```

2. Enabled internet access for the app
Under manifests --> AndroidManifest.xml tillades nedanstående kod för att tillgängliggöra
och erbjuda internet tillgång.
```
<uses-permission android:name="android.permission.INTERNET" />
```

3. Create WebView element
Inom res --> layout --> content_main.xml tillades nedantående kod för att skapa en webview till
applikationen.

```
  <WebView
        android:id="@+id/webview"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        />
 ```

4. Gave Webview an ID
Inom res --> layout --> content_main.xml ändrades id från webview till my_webview
```
  <WebView
        android:id="@+id/my_webview"
        ...
```

5. Created and located private variable, created WebViewClient.
Under MainActivity tillades koden tillsammans med dess importerade klasser.
setWebViewClient tillades för att öppna hemsidan samt dess länkar inuti applikationen.
Ett ID tillades för att kunna referera till elementet i nästa steg vid uppvisning av web page.

```
    // Private member
    private WebView myWebView;
   ...
        WebView myWebView = (WebView) findViewById(R.id.my_webview);

        WebViewClient myWebViewClient = new WebViewClient();
        myWebView.setWebViewClient(myWebViewClient);

    ```


6. Enabled Javascript and added url.
Javascript tillgängligjordes med nedanstående kod.
Därefter specificerades vilken url som skulle öppnas upp lokalt i applikationen.
```
        WebSettings webSettings = myWebView.getSettings();
        webSettings.setJavaScriptEnabled(true);

        myWebView.loadUrl("https://his.se");
```
file:///android_asset/img/local.png
Bild 1: Demonstrerar den lokala webbsidan.


7. External Webpage
En External webpage tillades genom nedanstående kod
```
    public void showExternalWebPage(){
        // TODO: Add your code for showing external web page here

        myWebView.loadUrl("https://www.his.se/forskning/");
    }
```
Som därefter kallades på genom:
```
        //noinspection SimplifiableIfStatement
        if (id == R.id.action_external_web) {
            showExternalWebPage();
            Log.d("==>","Will display external web page");
            return true;
        }
```
file:///android_asset/img/external.png
Bild 2: Uppvisar den externa webbsidan.

8. Internal Webpage
En Internal webpage tillades genom nedanstående kod. En egen konstruerad html sida skapades vilken
skickade information  mellan applikation och webbsida. Den konstruerades på grund av säkerhetsskäl
samt för att öka kontrollen. Sidan tillades genom att skapa en lokal asset mapp vilken html filen
skapades inuti. En top margin lades till.

```
   public void showInternalWebPage(){
        // TODO: Add your code for showing internal web page here

        myWebView.loadUrl("file:///android_asset/about.html");
    }
```

och som kallades på i:
```
        if (id == R.id.action_internal_web) {
            showInternalWebPage();
            Log.d("==>","Will display internal web page");
            return true;
        }
```

file:///android_asset/img/internal.png
Bild 3: Uppvisar den interna webbsidan.


