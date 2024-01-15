When storing SVG in a MongoDB database, you can model it as a document with at least two key fields: one for the SVG content and another for metadata or additional information. Here's a simple example using a "svgDocuments" collection:

```javascript
// MongoDB document model
const svgDocumentSchema = new mongoose.Schema({
  title: {
    type: String,
    required: true,
  },
  svgContent: {
    type: String,
    required: true,
  },
  description: String,
  createdAt: {
    type: Date,
    default: Date.now,
  },
});

// MongoDB collection model
const SvgDocument = mongoose.model('SvgDocument', svgDocumentSchema);
```

In this example:

- `title`: Represents the title or name of the SVG document.
- `svgContent`: Stores the actual SVG content as a string.
- `description`: An optional field to include a description of the SVG document.
- `createdAt`: Automatically tracks the creation timestamp.

When saving an SVG document to the database, you can create a new instance of the `SvgDocument` model and then save it:

```javascript
const newSvgDocument = new SvgDocument({
  title: 'My SVG',
  svgContent: '<svg xmlns="http://www.w3.org/2000/svg" width="100" height="100"><circle cx="50" cy="50" r="40" fill="red" /></svg>',
  description: 'An example SVG document',
});

newSvgDocument.save()
  .then((savedDocument) => {
    console.log('SVG document saved:', savedDocument);
  })
  .catch((error) => {
    console.error('Error saving SVG document:', error);
  });
```

Remember to replace the example SVG content with the actual SVG data you want to store. Additionally, consider adjusting the schema based on your application's specific requirements.

Make sure to handle validation, sanitization, and security measures when dealing with user-generated SVG content to prevent potential security risks like Cross-Site Scripting (XSS).