# AI कोड समीक्षक

AI कोड समीक्षक एक GitHub Action है जो आपके पुल रिक्वेस्ट पर बुद्धिमान फीडबैक और सुझाव प्रदान करने के लिए OpenAI के GPT-4 API का उपयोग करता है। यह शक्तिशाली टूल कोड गुणवत्ता में सुधार करने में मदद करता है और कोड समीक्षा प्रक्रिया को स्वचालित करके डेवलपर्स का समय बचाता है।

## विशेषताएं

- OpenAI के GPT-4 API का उपयोग करके पुल रिक्वेस्ट की समीक्षा करता है।
- आपके कोड को बेहतर बनाने के लिए बुद्धिमान टिप्पणियां और सुझाव प्रदान करता है।
- निर्दिष्ट exclude पैटर्न से मेल खाने वाली फाइलों को फ़िल्टर करता है।
- आपके GitHub वर्कफ़्लो में सेटअप और एकीकरण करना आसान है।

## सेटअप

1. इस GitHub Action का उपयोग करने के लिए, आपको एक OpenAI API key की आवश्यकता है। यदि आपके पास एक नहीं है, तो
   [OpenAI](https://beta.openai.com/signup) पर API key के लिए साइन अप करें।

2. OpenAI API key को अपने रिपॉजिटरी में `OPENAI_API_KEY` नाम से GitHub Secret के रूप में जोड़ें। आप GitHub Secrets के बारे में अधिक
   जानकारी [यहां](https://docs.github.com/en/actions/reference/encrypted-secrets) पा सकते हैं।

3. अपने रिपॉजिटरी में एक `.github/workflows/main.yml` फाइल बनाएं और निम्नलिखित सामग्री जोड़ें:

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
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }} # GITHUB_TOKEN डिफ़ॉल्ट रूप से मौजूद है इसलिए आपको इसे वैसे ही रखना होगा और इसे secret के रूप में जोड़ने की आवश्यकता नहीं है क्योंकि यह एक error देगा। [अधिक विवरण](https://docs.github.com/en/actions/security-guides/automatic-token-authentication#about-the-github_token-secret)
          OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}
          OPENAI_API_MODEL: "gpt-4" # वैकल्पिक: डिफ़ॉल्ट "gpt-4" है
          exclude: "**/*.json, **/*.md" # वैकल्पिक: कॉमा से अलग किए गए exclude पैटर्न
```

4. `your-username` को अपने GitHub username या organization name से बदलें जहां AI Code Reviewer रिपॉजिटरी स्थित है।

5. यदि आप कुछ फाइल पैटर्न को समीक्षा से बाहर रखना चाहते हैं तो `exclude` इनपुट को कस्टमाइज़ करें।

6. परिवर्तनों को अपने रिपॉजिटरी में commit करें, और AI Code Reviewer आपके भविष्य के पुल रिक्वेस्ट पर काम करना शुरू कर देगा।

## यह कैसे काम करता है

AI Code Reviewer GitHub Action पुल रिक्वेस्ट diff को पुनर्प्राप्त करता है, excluded फाइलों को फ़िल्टर करता है, और कोड chunks को
OpenAI API को भेजता है। फिर यह AI की प्रतिक्रिया के आधार पर समीक्षा टिप्पणियां उत्पन्न करता है और उन्हें पुल रिक्वेस्ट में जोड़ता है।

## योगदान

योगदान का स्वागत है! AI Code Reviewer GitHub Action को बेहतर बनाने के लिए कृपया बेझिझक issues या पुल रिक्वेस्ट सबमिट करें।

maintainer को अंतिम package उत्पन्न करने दें (`yarn build` & `yarn package`)।

## लाइसेंस

यह प्रोजेक्ट MIT License के तहत लाइसेंस प्राप्त है। अधिक जानकारी के लिए [LICENSE](LICENSE) फाइल देखें।
