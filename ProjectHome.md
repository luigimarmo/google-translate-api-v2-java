# Google Translate API v2 Java #

An unofficial Java wrapper for Google Translate API v2 (http://code.google.com/apis/language/translate/v2/getting_started.html) - Provides a full comprehensive access to all the API features.

Among the applications using this project:
  * [Google Translate Desktop](http://code.google.com/p/google-translate-desktop/) - a free unofficial Java desktop client based on Google Translate service.
_If you are using this project and you would like to be added here, please email me._

<br>

The project consists of two modules:<br>
<ul><li><b><a href='http://code.google.com/p/google-translate-api-v2-java/#Core'>Core</a></b> - Contains full comprehensive access to all the API functionality.<br>
</li><li><b><a href='http://code.google.com/p/google-translate-api-v2-java/#CLI'>CLI</a></b> - Uses the Core module to gain full comprehensive access to all the API functionality using a Command Line Interface.</li></ul>

<b>Quick links:</b>
<ul><li><a href='http://google-translate-api-v2-java.googlecode.com/svn/trunk/resources/latest-javadoc/index.html'>Java Docs</a>
</li><li><a href="http://code.google.com/p/google-translate-api-v2-java/#What's_new?">What's_new? / Changelog</a></li></ul>

<h2>Core</h2>

Contains full comprehensive access to all the API functionality. The application needs only to create a Translator instance and start using the API methods:<br>
<br>
<pre><code>/**<br>
     * Lists the supported languages. These languages can be used as the values of the sourceLanguage and targetLanguage<br>
     * for the different API methods.<br>
     *<br>
     * @param targetLanguage Language code - If not null, the list of supported languages will contain the name of the language in the targetLanguage<br>
     * @return Array of supported languages<br>
     * @throws URISyntaxException  In case of a malformed URI<br>
     * @throws IOException         In case of an HTTP exception<br>
     * @throws TranslatorException In case Google Translate API returned an error.<br>
     */<br>
    public Language[] languages(String targetLanguage) throws URISyntaxException, IOException, TranslatorException<br>
</code></pre>

<pre><code>/**<br>
     * Translating sourceText from sourceLanguage to targetLanguage.<br>
     *<br>
     * @param sourceTexts    Texts to translate - each text can be in a different language (The total size of the texts<br>
     *                       must be 5K or less due to Google Translate API limitations)<br>
     * @param sourceLanguage The language code of the source text or null for auto detection.<br>
     * @param targetLanguage The language code to translate to.<br>
     * @return The translation results.<br>
     * @throws URISyntaxException  In case of a malformed URI<br>
     * @throws IOException         In case of an HTTP exception<br>
     * @throws TranslatorException In case Google Translate API returned an error.<br>
     */<br>
    public Translation[] translate(String[] sourceTexts, String sourceLanguage, String targetLanguage) throws URISyntaxException, IOException, TranslatorException<br>
</code></pre>

<pre><code>/**<br>
     * Detects the language of a text.<br>
     *<br>
     * @param sourceTexts Texts to detect - each text can be in a different language (The total size of the texts<br>
     *                    must be 5K or less due to Google Translate API limitations)<br>
     * @return Matrix of detections - each detections[i] corresponds to sourceTexts[i] - if sourceTexts[i] can be<br>
     *         associated with more than one language, detections[i] can contain multiple Detection objects.<br>
     * @throws URISyntaxException  In case of a malformed URI<br>
     * @throws IOException         In case of an HTTP exception<br>
     * @throws TranslatorException In case Google Translate API returned an error.<br>
     */<br>
    public Detection[][] detect(String[] sourceTexts) throws URISyntaxException, IOException, TranslatorException<br>
</code></pre>

<pre><code><br>
package org.google.translate.api.v2.core;<br>
<br>
import org.google.translate.api.v2.core.model.Detection;<br>
import org.google.translate.api.v2.core.model.Language;<br>
import org.google.translate.api.v2.core.model.Translation;<br>
<br>
import java.io.IOException;<br>
import java.net.URISyntaxException;<br>
import java.util.Arrays;<br>
<br>
public class TranslatorTest {<br>
<br>
    private static Translator translator;<br>
<br>
    public static void main(String[] args) throws IOException, URISyntaxException {<br>
        if (args.length != 1) {<br>
            System.out.println("Google API key must be passed as the first and last argument");<br>
            System.exit(1);<br>
        }<br>
<br>
        translator = new Translator(args[0]);<br>
        try {<br>
            testLanguages();<br>
            testTranslate();<br>
            testDetect();<br>
        } catch (TranslatorException e) {<br>
            System.out.println("Google Translate API returned an error " + e.getMessage());<br>
            e.printStackTrace();<br>
        } finally {<br>
            translator.close();<br>
        }<br>
    }<br>
<br>
    /**<br>
     * Tests the {@link Translator#languages(String)} method.<br>
     *<br>
     * @throws URISyntaxException  In case of a malformed URI<br>
     * @throws IOException         In case of an HTTP exception<br>
     * @throws TranslatorException In case Google Translate API returned an error.<br>
     */<br>
    public static void testLanguages() throws IOException, URISyntaxException, TranslatorException {<br>
        Language[] languages = translator.languages("en"); // Returns a list of supported languages with the language name in English<br>
        System.out.println("languages = " + Arrays.toString(languages));<br>
        // OUTPUT: languages = [Language{language='af', name='Afrikaans'}, Language{language='sq', name='Albanian'}, Language{language='ar', name='Arabic'}, Language{language='be', name='Belarusian'}, Language{language='bg', name='Bulgarian'}, Language{language='ca', name='Catalan'}, Language{language='zh', name='Chinese (Simplified)'}, Language{language='zh-TW', name='Chinese (Traditional)'}, Language{language='hr', name='Croatian'}, Language{language='cs', name='Czech'}, Language{language='da', name='Danish'}, Language{language='nl', name='Dutch'}, Language{language='en', name='English'}, Language{language='et', name='Estonian'}, Language{language='tl', name='Filipino'}, Language{language='fi', name='Finnish'}, Language{language='fr', name='French'}, Language{language='gl', name='Galician'}, Language{language='de', name='German'}, Language{language='el', name='Greek'}, Language{language='ht', name='Haitian Creole'}, Language{language='iw', name='Hebrew'}, Language{language='hi', name='Hindi'}, Language{language='hu', name='Hungarian'}, Language{language='is', name='Icelandic'}, Language{language='id', name='Indonesian'}, Language{language='ga', name='Irish'}, Language{language='it', name='Italian'}, Language{language='ja', name='Japanese'}, Language{language='ko', name='Korean'}, Language{language='lv', name='Latvian'}, Language{language='lt', name='Lithuanian'}, Language{language='mk', name='Macedonian'}, Language{language='ms', name='Malay'}, Language{language='mt', name='Maltese'}, Language{language='no', name='Norwegian'}, Language{language='fa', name='Persian'}, Language{language='pl', name='Polish'}, Language{language='pt', name='Portuguese'}, Language{language='ro', name='Romanian'}, Language{language='ru', name='Russian'}, Language{language='sr', name='Serbian'}, Language{language='sk', name='Slovak'}, Language{language='sl', name='Slovenian'}, Language{language='es', name='Spanish'}, Language{language='sw', name='Swahili'}, Language{language='sv', name='Swedish'}, Language{language='th', name='Thai'}, Language{language='tr', name='Turkish'}, Language{language='uk', name='Ukrainian'}, Language{language='vi', name='Vietnamese'}, Language{language='cy', name='Welsh'}, Language{language='yi', name='Yiddish'}]<br>
    }<br>
<br>
    /**<br>
     * Tests the {@link Translator#translate(String, String, String)} and {@link Translator#translate(String[], String, String)} methods.<br>
     *<br>
     * @throws URISyntaxException  In case of a malformed URI<br>
     * @throws IOException         In case of an HTTP exception<br>
     * @throws TranslatorException In case Google Translate API returned an error.<br>
     */<br>
    public static void testTranslate() throws IOException, URISyntaxException, TranslatorException {<br>
        // Translate "I" from unknown (auto-detect) to Spanish<br>
        Translation fromEnglish = translator.translate("I", "en", "es");<br>
        System.out.println("'I' in en = '" + fromEnglish.getTranslatedText() + "' in es");<br>
        // OUTPUT: 'I' in en = 'Yo' in es<br>
<br>
<br>
        // Translate "I" from unknown (auto-detect) to Spanish<br>
        Translation fromUnknown = translator.translate("I", null, "es");<br>
        System.out.println("'I' in " + fromUnknown.getDetectedSourceLanguage() + " = '" + fromUnknown.getTranslatedText() + "' in es");<br>
        // OUTPUT: 'I' in no = 'En' in es<br>
<br>
        // Translate multiple source text strings<br>
        String[] sourceTexts = {"I", "a"};<br>
        Translation[] translations = translator.translate(sourceTexts, null, "es");<br>
        for (int i = 0, sourceTextsLength = sourceTexts.length; i &lt; sourceTextsLength; i++) {<br>
            System.out.println("'" + sourceTexts[i] + "' in en = " + "'" + translations[i].getTranslatedText() + "' in es");<br>
        }<br>
        // OUTPUT: 'I' in en = 'En' in es<br>
        //         'a' in en = 'un' in es<br>
    }<br>
<br>
    /**<br>
     * Tests the {@link Translator#detect(String[])} method.<br>
     *<br>
     * @throws URISyntaxException  In case of a malformed URI<br>
     * @throws IOException         In case of an HTTP exception<br>
     * @throws TranslatorException In case Google Translate API returned an error.<br>
     */<br>
    private static void testDetect() throws IOException, URISyntaxException, TranslatorException {<br>
        Detection[][] detections = translator.detect(new String[]{"I", "We"});<br>
        System.out.println("detections = " + Arrays.deepToString(detections));<br>
        // OUTPUT: detections = [[Detection{language='no', reliable=false, confidence=0.09615925}], [Detection{language='en', reliable=false, confidence=0.08430534}]]<br>
    }<br>
}<br>
</code></pre>


<h2>CLI</h2>

Uses the Core module to gain full comprehensive access to all the API functionality using a Command Line Interface.<br>
<br>
<pre><code><br>
java -jar google-translate-api-v2-java-cli-0.51.jar<br>
<br>
Google Translate API v2 CLI version 0.51, Google Translate API v2 version 0.51<br>
usage: java -jar google-translate-api-v2-java-cli-0.5.jar [-ak &lt;api-key&gt;]<br>
       [-d &lt;source-texts&gt;] [-h] [-l] [-o &lt;format&gt;] [-sl &lt;language&gt;] [-t<br>
       &lt;source-texts&gt;] [-tl &lt;language&gt;] [-v] [-verbose]<br>
 -ak,--apiKey &lt;api-key&gt;            Every request your application sends to<br>
                                   the Google Translate API must identify<br>
                                   your application to Google, using an<br>
                                   API key (http://code.google.com/apis/language/translate/v2/using_rest.html#auth). <br>
                                   Use the 'apiKey' option or the<br>
                                   'GOOGLE_API_KEY' environment variable<br>
 -d,--detect &lt;source-texts&gt;        Detects the language of source texts<br>
 -h,--help                         Shows this help message<br>
 -l,--languages                    Shows the supported languages that can<br>
                                   be used in 'sourceLanguage' and<br>
                                   'targetLanguage' options. Can be used<br>
                                   with the 'targetLanguage' to show the<br>
                                   names of the supported languages in<br>
                                   addition to the codes<br>
 -o,--output &lt;format&gt;              The format of the output. Possible<br>
                                   values are 'plain' (default), 'xml',<br>
                                   'json'<br>
 -sl,--sourceLanguage &lt;language&gt;   The language code of the source<br>
                                   language. Used with the 'translate'<br>
                                   option as the language from which to<br>
                                   translate. If not mentioned, the source<br>
                                   language will be auto detected<br>
 -t,--translate &lt;source-texts&gt;     Translates source texts. Must be used<br>
                                   with the 'targetLanguage' to indicate<br>
                                   the language to translate to, can also<br>
                                   be used with the optional<br>
                                   'sourceLanguage' option<br>
 -tl,--targetLanguage &lt;language&gt;   The language code of the target<br>
                                   language. Mandatory when using with the<br>
                                   'translate' option, optional when using<br>
                                   with the 'languages' option<br>
 -v,--version                      Shows the version of the TranslatorCli<br>
                                   and Translator core<br>
 -verbose                          Outputs more detailed information that<br>
                                   can help troubleshooting<br>
Examples:<br>
--apiKey YOUR_GOOGLE_API_KEY --translate "Hello" "Hola" --targetLanguage iw<br>
--apiKey YOUR_GOOGLE_API_KEY --detect "Hello" "Hola" --output xml<br>
--apiKey YOUR_GOOGLE_API_KEY --languages --targetLanguage en<br>
<br>
</code></pre>


<br>

<h1>What's new?</h1>

<b>Version 0.52</b>

<ul><li>Internally splitting sourceTexts to avoid "Too many text segments" Google Translate API error.<br>
</li></ul><blockquote>The splitting and sending is done internally in the translate and detect methods so there is no limitation of the length of sourceTexts as far as the user is concerned.<br>
</blockquote><ul><li>Adding <code>location</code> and <code>locationType</code> to <code>ApiError.ErrorEntry</code></li></ul>

<b>Version 0.51</b>

<ul><li>Changing default toString behaviour in the core module to allow easier usage in applications.<br>
<ul><li><code>Translation.toString()</code> returns the translatedText<br>
</li><li><code>Detection.toString()</code> returns the language<br>
</li><li><code>Language.toString()</code> returns the name or the language if the name is null.<br>
</li></ul></li></ul><blockquote>The plain output format of the CLI module was not changed.<br>
The toString format can be determined by the "org.google.translate.api.v2.core.model.toString" Java property described below.<br>
</blockquote><ul><li>Adding the "org.google.translate.api.v2.core.model.toString" Java property.<br>
</li></ul><blockquote>Allowed values are:<br>
<ul><li>short - returns the most simple and important info (Default when using the core module).<br>
</li><li>long - returns all the not null fields.<br>
</li><li>full - returns all the fields (Default when using the CLI module).<br>
</li></ul>A constant with the property name can be found at <code>org.google.translate.api.v2.core.model.AbstractResponseObject.TO_STRING_FORMAT</code>.<br>
</blockquote><ul><li>Adding ability to pass the Google API key to the CLI module using an environment variable "GOOGLE_API_KEY" instead of the apiKey option.<br>
</li></ul><blockquote>If both are available, the apiKey option will be used.<br>
A constant with the env var name can be found at <code>org.google.translate.api.v2.cli.TranslatorCli.GOOGLE_API_KEY</code>.<br>
</blockquote><ul><li>Adding the verbose option to allow more detailed info to assist troubleshooting.</li></ul>

<b>Version 0.5</b>

<ul><li>translate	- Translates source text(s) from source language to target language.<br>
</li><li>languages	- List the source and target languages supported by the translate methods.<br>
</li><li>detect      - Detect language of source text(s).