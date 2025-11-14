# AI कोड रिव्यूअर

AI कोड रिव्यूअर एक GitHub Action है जो OpenAI के GPT-4 API का उपयोग करके आपके पुल रिक्वेस्ट पर बुद्धिमान फीडबैक और सुझाव प्रदान करता है। यह शक्तिशाली टूल कोड गुणवत्ता में सुधार करने में मदद करता है और कोड रिव्यू प्रक्रिया को स्वचालित करके डेवलपर्स का समय बचाता है।

## विशेषताएँ

- OpenAI के GPT-4 API का उपयोग करके पुल रिक्वेस्ट की समीक्षा करता है।
- आपके कोड में सुधार के लिए बुद्धिमान टिप्पणियाँ और सुझाव प्रदान करता है।
- निर्दिष्ट बहिष्करण पैटर्न से मेल खाने वाली फाइलों को फ़िल्टर करता है।
- आपके GitHub वर्कफ्लो में आसानी से सेट अप और एकीकृत करने योग्य।

## सेटअप

1. इस GitHub Action का उपयोग करने के लिए, आपको एक OpenAI API कुंजी की आवश्यकता है। यदि आपके पास नहीं है, तो [OpenAI](https://beta.openai.com/signup) पर साइन अप करके एक API कुंजी प्राप्त करें।

2. OpenAI API कुंजी को अपने रिपॉजिटरी में `OPENAI_API_KEY` नाम से GitHub Secret के रूप में जोड़ें। GitHub Secrets के बारे में अधिक जानकारी [यहाँ](https://docs.github.com/en/actions/reference/encrypted-secrets) मिल सकती है।

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

4. `your-username` को अपने GitHub उपयोगकर्ता नाम या संगठन के नाम से बदलें जहाँ AI Code Reviewer रिपॉजिटरी स्थित है।

5. यदि आप कुछ फाइल पैटर्न को समीक्षा से बाहर रखना चाहते हैं, तो `exclude` इनपुट को अनुकूलित करें।

6. अपने रिपॉजिटरी में परिवर्तनों को कमिट करें, और AI Code Reviewer आपके भविष्य के पुल रिक्वेस्ट पर काम करना शुरू कर देगा।

## यह कैसे काम करता है

AI Code Reviewer GitHub Action पुल रिक्वेस्ट diff को पुनः प्राप्त करता है, बहिष्कृत फाइलों को फ़िल्टर करता है, और कोड चंक को OpenAI API को भेजता है। फिर यह AI के प्रतिसाद के आधार पर समीक्षा टिप्पणियाँ उत्पन्न करता है और उन्हें पुल रिक्वेस्ट में जोड़ता है।

## योगदान

योगदान स्वागत योग्य हैं! कृपया AI Code Reviewer GitHub Action में सुधार के लिए मुद्दे या पुल रिक्वेस्ट सबमिट करने के लिए स्वतंत्र महसूस करें।

अंतिम पैकेज उत्पन्न करने के लिए मैनटेनर को अनुमति दें (`yarn build` & `yarn package`)।

## लाइसेंस

यह प्रोजेक्ट MIT License के तहत लाइसेंस प्राप्त है। अधिक जानकारी के लिए [LICENSE](LICENSE) फाइल देखें।