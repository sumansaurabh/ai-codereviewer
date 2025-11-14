# एआई कोड रिव्यूअर

एआई कोड रिव्यूअर एक गिटहब एक्शन है जो ओपनएआई के जीपीटी-4 एपीआई का उपयोग करके आपके पुल रिक्वेस्ट पर बुद्धिमान फीडबैक और सुझाव प्रदान करता है। यह शक्तिशाली टूल कोड गुणवत्ता में सुधार करने में मदद करता है और कोड रिव्यू प्रक्रिया को स्वचालित करके डेवलपर्स का समय बचाता है।

## विशेषताएँ

- ओपनएआई के जीपीटी-4 एपीआई का उपयोग करके पुल रिक्वेस्ट की समीक्षा करता है।
- आपके कोड में सुधार के लिए बुद्धिमान टिप्पणियाँ और सुझाव प्रदान करता है।
- निर्दिष्ट बहिष्करण पैटर्न से मेल खाने वाली फाइलों को फ़िल्टर करता है।
- आपके गिटहब वर्कफ्लो में आसानी से सेट अप और एकीकृत करना।

## सेटअप

1. इस गिटहब एक्शन का उपयोग करने के लिए, आपको एक ओपनएआई एपीआई कुंजी की आवश्यकता है। यदि आपके पास नहीं है, तो [ओपनएआई](https://beta.openai.com/signup) पर साइन अप करें।

2. ओपनएआई एपीआई कुंजी को आपके रिपॉजिटरी में `OPENAI_API_KEY` नाम से गिटहब सीक्रेट के रूप में जोड़ें। गिटहब सीक्रेट के बारे में अधिक जानकारी [यहाँ](https://docs.github.com/en/actions/reference/encrypted-secrets) मिल सकती है।

3. अपने रिपॉजिटरी में `.github/workflows/main.yml` फाइल बनाएं और निम्नलिखित सामग्री जोड़ें:

```yaml
name: AI Code Reviewer

on:
  pull_request:
    types:
      - opened
      - synchronize
permissions: write-all
jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repo
        uses: actions/checkout@v3

      - name: AI Code Reviewer
        uses: your-username/ai-code-reviewer@main
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }} # The GITHUB_TOKEN is there by default so you just need to keep it like it is and not necessarily need to add it as secret as it will throw an error. [More Details](https://docs.github.com/en/actions/security-guides/automatic-token-authentication#about-the-github_token-secret)
          OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}
          OPENAI_API_MODEL: "gpt-4" # Optional: defaults to "gpt-4"
          exclude: "**/*.json, **/*.md" # Optional: exclude patterns separated by commas
```

4. `your-username` को अपने गिटहब यूजरनेम या संगठन के नाम से बदलें जहाँ एआई कोड रिव्यूअर रिपॉजिटरी स्थित है।

5. यदि आप कुछ फाइल पैटर्न को समीक्षा से बाहर रखना चाहते हैं तो `exclude` इनपुट को कस्टमाइज़ करें।

6. अपने रिपॉजिटरी में परिवर्तनों को कमिट करें, और एआई कोड रिव्यूअर आपके भविष्य के पुल रिक्वेस्ट पर काम करना शुरू कर देगा।

## यह कैसे काम करता है

एआई कोड रिव्यूअर गिटहब एक्शन पुल रिक्वेस्ट डिफ को पुनः प्राप्त करता है, बहिष्कृत फाइलों को फ़िल्टर करता है, और कोड चंक को ओपनएआई एपीआई में भेजता है। फिर यह एआई के प्रतिसाद के आधार पर समीक्षा टिप्पणियाँ उत्पन्न करता है और उन्हें पुल रिक्वेस्ट में जोड़ता है।

## योगदान

योगदान स्वागत योग्य हैं! कृपया एआई कोड रिव्यूअर गिटहब एक्शन में सुधार के लिए मुद्दे या पुल रिक्वेस्ट सबमिट करने में संकोच न करें।

मुख्य रखरखावकर्ता को अंतिम पैकेज उत्पन्न करने दें (`yarn build` & `yarn package`)।

## लाइसेंस

यह प्रोजेक्ट एमआईटी लाइसेंस के तहत लाइसेंस प्राप्त है। अधिक जानकारी के लिए [लाइसेंस](LICENSE) फाइल देखें।