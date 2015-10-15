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
<pre><code>/**
     * Lists the supported languages. These languages can be used as the values of the sourceLanguage and targetLanguage
     * for the different API methods.
     *
     * @param targetLanguage Language code - If not null, the list of supported languages will contain the name of the language in the targetLanguage
     * @return Array of supported languages
     * @throws URISyntaxException  In case of a malformed URI
     * @throws IOException         In case of an HTTP exception
     * @throws TranslatorException In case Google Translate API returned an error.
     */
    public Language[] languages(String targetLanguage) throws URISyntaxException, IOException, TranslatorException
</code></pre>

<pre><code>/**
     * Translating sourceText from sourceLanguage to targetLanguage.
     *
     * @param sourceTexts    Texts to translate - each text can be in a different language (The total size of the texts
     *                       must be 5K or less due to Google Translate API limitations)
     * @param sourceLanguage The language code of the source text or null for auto detection.
     * @param targetLanguage The language code to translate to.
     * @return The translation results.
     * @throws URISyntaxException  In case of a malformed URI
     * @throws IOException         In case of an HTTP exception
     * @throws TranslatorException In case Google Translate API returned an error.
     */
    public Translation[] translate(String[] sourceTexts, String sourceLanguage, String targetLanguage) throws URISyntaxException, IOException, TranslatorException
</code></pre>

<pre><code>/**
     * Detects the language of a text.
     *
     * @param sourceTexts Texts to detect - each text can be in a different language (The total size of the texts
     *                    must be 5K or less due to Google Translate API limitations)
     * @return Matrix of detections - each detections[i] corresponds to sourceTexts[i] - if sourceTexts[i] can be
     *         associated with more than one language, detections[i] can contain multiple Detection objects.
     * @throws URISyntaxException  In case of a malformed URI
     * @throws IOException         In case of an HTTP exception
     * @throws TranslatorException In case Google Translate API returned an error.
     */
    public Detection[][] detect(String[] sourceTexts) throws URISyntaxException, IOException, TranslatorException
</code></pre>

<pre><code>
package org.google.translate.api.v2.core;

import org.google.translate.api.v2.core.model.Detection;
import org.google.translate.api.v2.core.model.Language;
import org.google.translate.api.v2.core.model.Translation;

import java.io.IOException;
import java.net.URISyntaxException;
import java.util.Arrays;

public class TranslatorTest {

    private static Translator translator;

    public static void main(String[] args) throws IOException, URISyntaxException {
        if (args.length != 1) {
            System.out.println("Google API key must be passed as the first and last argument");
            System.exit(1);
        }

        translator = new Translator(args[0]);
        try {
            testLanguages();
            testTranslate();
            testDetect();
        } catch (TranslatorException e) {
            System.out.println("Google Translate API returned an error " + e.getMessage());
            e.printStackTrace();
        } finally {
            translator.close();
        }
    }

    /**
     * Tests the {@link Translator#languages(String)} method.
     *
     * @throws URISyntaxException  In case of a malformed URI
     * @throws IOException         In case of an HTTP exception
     * @throws TranslatorException In case Google Translate API returned an error.
     */
    public static void testLanguages() throws IOException, URISyntaxException, TranslatorException {
        Language[] languages = translator.languages("en"); // Returns a list of supported languages with the language name in English
        System.out.println("languages = " + Arrays.toString(languages));
        // OUTPUT: languages = [Language{language='af', name='Afrikaans'}, Language{language='sq', name='Albanian'}, Language{language='ar', name='Arabic'}, Language{language='be', name='Belarusian'}, Language{language='bg', name='Bulgarian'}, Language{language='ca', name='Catalan'}, Language{language='zh', name='Chinese (Simplified)'}, Language{language='zh-TW', name='Chinese (Traditional)'}, Language{language='hr', name='Croatian'}, Language{language='cs', name='Czech'}, Language{language='da', name='Danish'}, Language{language='nl', name='Dutch'}, Language{language='en', name='English'}, Language{language='et', name='Estonian'}, Language{language='tl', name='Filipino'}, Language{language='fi', name='Finnish'}, Language{language='fr', name='French'}, Language{language='gl', name='Galician'}, Language{language='de', name='German'}, Language{language='el', name='Greek'}, Language{language='ht', name='Haitian Creole'}, Language{language='iw', name='Hebrew'}, Language{language='hi', name='Hindi'}, Language{language='hu', name='Hungarian'}, Language{language='is', name='Icelandic'}, Language{language='id', name='Indonesian'}, Language{language='ga', name='Irish'}, Language{language='it', name='Italian'}, Language{language='ja', name='Japanese'}, Language{language='ko', name='Korean'}, Language{language='lv', name='Latvian'}, Language{language='lt', name='Lithuanian'}, Language{language='mk', name='Macedonian'}, Language{language='ms', name='Malay'}, Language{language='mt', name='Maltese'}, Language{language='no', name='Norwegian'}, Language{language='fa', name='Persian'}, Language{language='pl', name='Polish'}, Language{language='pt', name='Portuguese'}, Language{language='ro', name='Romanian'}, Language{language='ru', name='Russian'}, Language{language='sr', name='Serbian'}, Language{language='sk', name='Slovak'}, Language{language='sl', name='Slovenian'}, Language{language='es', name='Spanish'}, Language{language='sw', name='Swahili'}, Language{language='sv', name='Swedish'}, Language{language='th', name='Thai'}, Language{language='tr', name='Turkish'}, Language{language='uk', name='Ukrainian'}, Language{language='vi', name='Vietnamese'}, Language{language='cy', name='Welsh'}, Language{language='yi', name='Yiddish'}]
    }

    /**
     * Tests the {@link Translator#translate(String, String, String)} and {@link Translator#translate(String[], String, String)} methods.
     *
     * @throws URISyntaxException  In case of a malformed URI
     * @throws IOException         In case of an HTTP exception
     * @throws TranslatorException In case Google Translate API returned an error.
     */
    public static void testTranslate() throws IOException, URISyntaxException, TranslatorException {
        // Translate "I" from unknown (auto-detect) to Spanish
        Translation fromEnglish = translator.translate("I", "en", "es");
        System.out.println("'I' in en = '" + fromEnglish.getTranslatedText() + "' in es");
        // OUTPUT: 'I' in en = 'Yo' in es


        // Translate "I" from unknown (auto-detect) to Spanish
        Translation fromUnknown = translator.translate("I", null, "es");
        System.out.println("'I' in " + fromUnknown.getDetectedSourceLanguage() + " = '" + fromUnknown.getTranslatedText() + "' in es");
        // OUTPUT: 'I' in no = 'En' in es

        // Translate multiple source text strings
        String[] sourceTexts = {"I", "a"};
        Translation[] translations = translator.translate(sourceTexts, null, "es");
        for (int i = 0, sourceTextsLength = sourceTexts.length; i &lt; sourceTextsLength; i++) {
            System.out.println("'" + sourceTexts[i] + "' in en = " + "'" + translations[i].getTranslatedText() + "' in es");
        }
        // OUTPUT: 'I' in en = 'En' in es
        //         'a' in en = 'un' in es
    }

    /**
     * Tests the {@link Translator#detect(String[])} method.
     *
     * @throws URISyntaxException  In case of a malformed URI
     * @throws IOException         In case of an HTTP exception
     * @throws TranslatorException In case Google Translate API returned an error.
     */
    private static void testDetect() throws IOException, URISyntaxException, TranslatorException {
        Detection[][] detections = translator.detect(new String[]{"I", "We"});
        System.out.println("detections = " + Arrays.deepToString(detections));
        // OUTPUT: detections = [[Detection{language='no', reliable=false, confidence=0.09615925}], [Detection{language='en', reliable=false, confidence=0.08430534}]]
    }
}
</code></pre>


<h2>CLI</h2>

Uses the Core module to gain full comprehensive access to all the API functionality using a Command Line Interface.<br>
<br>
<pre><code>
java -jar google-translate-api-v2-java-cli-0.51.jar

Google Translate API v2 CLI version 0.51, Google Translate API v2 version 0.51
usage: java -jar google-translate-api-v2-java-cli-0.5.jar [-ak &lt;api-key&gt;]
       [-d &lt;source-texts&gt;] [-h] [-l] [-o &lt;format&gt;] [-sl &lt;language&gt;] [-t
       &lt;source-texts&gt;] [-tl &lt;language&gt;] [-v] [-verbose]
 -ak,--apiKey &lt;api-key&gt;            Every request your application sends to
                                   the Google Translate API must identify
                                   your application to Google, using an
                                   API key (http://code.google.com/apis/language/translate/v2/using_rest.html#auth). 
                                   Use the 'apiKey' option or the
                                   'GOOGLE_API_KEY' environment variable
 -d,--detect &lt;source-texts&gt;        Detects the language of source texts
 -h,--help                         Shows this help message
 -l,--languages                    Shows the supported languages that can
                                   be used in 'sourceLanguage' and
                                   'targetLanguage' options. Can be used
                                   with the 'targetLanguage' to show the
                                   names of the supported languages in
                                   addition to the codes
 -o,--output &lt;format&gt;              The format of the output. Possible
                                   values are 'plain' (default), 'xml',
                                   'json'
 -sl,--sourceLanguage &lt;language&gt;   The language code of the source
                                   language. Used with the 'translate'
                                   option as the language from which to
                                   translate. If not mentioned, the source
                                   language will be auto detected
 -t,--translate &lt;source-texts&gt;     Translates source texts. Must be used
                                   with the 'targetLanguage' to indicate
                                   the language to translate to, can also
                                   be used with the optional
                                   'sourceLanguage' option
 -tl,--targetLanguage &lt;language&gt;   The language code of the target
                                   language. Mandatory when using with the
                                   'translate' option, optional when using
                                   with the 'languages' option
 -v,--version                      Shows the version of the TranslatorCli
                                   and Translator core
 -verbose                          Outputs more detailed information that
                                   can help troubleshooting
Examples:
--apiKey YOUR_GOOGLE_API_KEY --translate "Hello" "Hola" --targetLanguage iw
--apiKey YOUR_GOOGLE_API_KEY --detect "Hello" "Hola" --output xml
--apiKey YOUR_GOOGLE_API_KEY --languages --targetLanguage en

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