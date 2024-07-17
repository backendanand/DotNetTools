# Setup
Install the following nuGet package
```
dotnet add package CoreHtmlToImage
```

## Create HTML file
```
<html>
    <head>
        <meta charset='UTF-8'>
    </head>
    <body>
        <h1>Name: {{Name}}</h1>
    </body>
</html>
```

## Create function
```
var htmlContent = System.IO.File.ReadAllText("Static/template.html");
htmlContent = htmlContent.Replace.Replace("{{Name}}", card.Name);
var image = await GenerateImageAsync(htmlContent);
return File(image, "image/png", $"Card_{card.CardNumber}.png");
```

```
private async Task<byte[]> GenerateImageAsync(string htmlContent)
{
    var converter = new HtmlConverter();
    var bytes = converter.FromHtmlString(htmlContent, 700, ImageFormat.Png);
    return bytes;
}
```
