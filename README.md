        public List<string> ReadPdfFile_1(string fileName)
        {
            List<String> text = new List<String>();
            String page;
            List<String> pageStrings;
            string[] separators = { "\n", "\r\n", "\t\n"};
            PdfReader reader = new PdfReader(fileName);
            for (int i = 1; i <= reader.NumberOfPages; i++)
            {
                ITextExtractionStrategy strategy = new LocationTextExtractionStrategy();
                page = PdfTextExtractor.GetTextFromPage(reader, i, strategy);
                pageStrings = new List<string>(page.Split(separators, StringSplitOptions.RemoveEmptyEntries));
                text.AddRange(pageStrings);

            }

            reader.Close();

            return text;
        }
        
        需要有itextsharp.dll，用到的引用有如下两个
        using iTextSharp.text.pdf;
using iTextSharp.text.pdf.parser;
