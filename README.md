# alu_regex-data-extraction-Obanijesu-ctrl
ALU Regex Data Extraction Project
This project implements a tool for extracting various data types from text using regular expressions.
Overview
The Regex Data Extractor is a command-line tool that can identify and extract the following data types from text:

Email addresses
URLs
Phone numbers
Credit card numbers
Time expressions (12-hour and 24-hour formats)
HTML tags
Hashtags
Currency amounts

The tool uses Python's re module with carefully crafted regular expressions to identify these patterns in text data.
Features

Extract multiple data types simultaneously
Process input from command line arguments or from text files
Interactive mode for quick testing
Option to save results to JSON file
Comprehensive error handling

Installation

Clone this repository:

bashgit clone https://github.com/your-username/alu_regex-data-extraction-YourUsername.git
cd alu_regex-data-extraction-YourUsername

No external dependencies are required beyond the Python standard library.

Usage
The script can be used in three different ways:
1. Interactive Mode
Run the script without any arguments:
bashpython regex_extractor.py
This will prompt you to enter text to analyze.
2. Text Input
Use the -t or --text argument to provide text directly:
bashpython regex_extractor.py -t "My email is sample@email.com and my website is https://example.org"
3. File Input
Use the -f or --file argument to process text from a file:
bashpython regex_extractor.py -f sample_text.txt
Saving Results
Add the -o or --output parameter to save results to a JSON file:
bashpython regex_extractor.py -t "Some text with patterns" -o results.json
Examples
Example 1: Extracting from Text
Command:
bashpython regex_extractor.py -t "Contact us at support@example.com or call (123) 456-7890. Visit https://example.org at 2:30 PM. #contact"
Output:
json{
  "emails": ["support@example.com"],
  "urls": ["https://example.org"],
  "phone_numbers": ["(123) 456-7890"],
  "credit_cards": [],
  "times": ["2:30 PM"],
  "html_tags": [],
  "hashtags": ["#contact"],
  "currency_amounts": []
}
Example 2: Extracting from File
Sample file content (test_data.txt):
Customer Information:
Email: john.doe@company.co.uk
Website: https://www.johndoe.com
Phone: 123.456.7890
CC: 1234-5678-9012-3456
Appointment: 14:30

<div class="profile">
  <p>Professional Profile</p>
</div>

#developer #python
Total due: $1,234.56
Command:
bashpython regex_extractor.py -f test_data.txt
Output:
json{
  "emails": ["john.doe@company.co.uk"],
  "urls": ["https://www.johndoe.com"],
  "phone_numbers": ["123.456.7890"],
  "credit_cards": ["1234-5678-9012-3456"],
  "times": ["14:30"],
  "html_tags": ["<div class=\"profile\">", "<p>Professional Profile</p>", "</div>"],
  "hashtags": ["#developer", "#python"],
  "currency_amounts": ["$1,234.56"]
}
Regular Expression Implementation
Email Addresses

Pattern: \b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}\b
Matches: user@example.com, firstname.lastname@company.co.uk

URLs

Pattern: https?:\/\/(?:www\.)?[-a-zA-Z0-9@:%._\+~#=]{1,256}\.[a-zA-Z0-9()]{1,6}\b(?:[-a-zA-Z0-9()@:%_\+.~#?&//=]*)
Matches: https://www.example.com, https://subdomain.example.org/page

Phone Numbers

Pattern: (?:\(\d{3}\)\s?|\d{3}[-.])\d{3}[-.]?\d{4}
Matches: (123) 456-7890, 123-456-7890, 123.456.7890

Credit Card Numbers

Pattern: \b\d{4}[\s-]?\d{4}[\s-]?\d{4}[\s-]?\d{4}\b
Matches: 1234 5678 9012 3456, 1234-5678-9012-3456

Times

Pattern: \b(?:(?:0?[1-9]|1[0-2]):[0-5][0-9]\s?(?:AM|PM|am|pm)|(?:[01]?[0-9]|2[0-3]):[0-5][0-9])\b
Matches: 14:30, 2:30 PM

HTML Tags

Pattern: <\/?[a-z][\s\S]*?>
Matches: <p>, <div class="example">, <img src="image.jpg" alt="description">

Hashtags

Pattern: #[a-zA-Z0-9_]+\b
Matches: #example, #ThisIsAHashtag

Currency Amounts

Pattern: \$\d{1,3}(?:,\d{3})*(?:\.\d{2})?
Matches: $19.99, $1,234.56

Edge Case Handling
The regular expressions have been designed to handle various edge cases:

Email validation handles different TLDs and subdomains
Phone number extraction supports multiple common formats
Currency amounts correctly handle thousands separators
HTML tag extraction works with both open and close tags, including attributes
Time extraction supports both 12-hour and 24-hour formats
