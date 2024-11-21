### A Quasar Project 
## Dynamic Form using JSON any one can create Form 

### Structure of the JSON should be like 
```bash
 {
  "fields": {
    "personalInfo": {
      "type": "q-accordion",
      "props": {
        "label": "Personal Information"
      },
      "children": {
        "firstName": {
          "type": "q-input",
          "props": {
            "label": "First Name",
            "outlined": true,
            "placeholder": "Enter your first name"
          }
        },
        "lastName": {
          "type": "q-input",
          "props": {
            "label": "Last Name",
            "outlined": true,
            "placeholder": "Enter your last name"
          }
        },
        "gender": {
          "type": "q-select",
          "props": {
            "label": "Gender",
            "options": [
              { "label": "Male", "value": "male" },
              { "label": "Female", "value": "female" },
              { "label": "Other", "value": "other" }
            ],
            "outlined": true,
            "emit-value": true,
            "map-options": true
          }
        }
      }
    },
    "preferences": {
      "type": "q-accordion",
      "props": {
        "label": "Preferences"
      },
      "children": {
        "notifications": {
          "type": "q-checkbox",
          "props": {
            "label": "Enable Notifications"
          }
        },
        "theme": {
          "type": "q-select",
          "props": {
            "label": "Theme",
            "options": [
              { "label": "Light", "value": "light" },
              { "label": "Dark", "value": "dark" }
            ],
            "outlined": true
          }
        }
      }
    },
    "contactInfo": {
      "type": "q-accordion",
      "props": {
        "label": "Contact Information"
      },
      "children": {
        "email": {
          "type": "q-input",
          "props": {
            "label": "Email",
            "type": "email",
            "outlined": true,
            "placeholder": "Enter your email"
          }
        },
        "phone": {
          "type": "q-input",
          "props": {
            "label": "Phone Number",
            "type": "tel",
            "outlined": true,
            "placeholder": "Enter your phone number"
          }
        }
      }
    },
    "survey": {
      "type": "q-accordion",
      "props": {
        "label": "Survey"
      },
      "children": {
        "satisfaction": {
          "type": "q-rating",
          "props": {
            "label": "Rate Your Satisfaction",
            "max": 5,
            "size": "lg"
          }
        },
        "suggestions": {
          "type": "q-input",
          "props": {
            "label": "Suggestions",
            "type": "textarea",
            "outlined": true,
            "rows": 5,
            "placeholder": "Enter your suggestions here"
          }
        }
      }
    }
  }
}
```
# Final Output Example
```bash
{
  "personalInfo": {
    "firstName": "John",
    "lastName": "Doe",
    "gender": "male"
  },
  "preferences": {
    "notifications": true,
    "theme": "dark"
  },
  "contactInfo": {
    "email": "john.doe@example.com",
    "phone": "123-456-7890"
  },
  "survey": {
    "satisfaction": 5,
    "suggestions": "Great job! Keep up the good work."
  }
}

```

# Quasar App (dynamic-formdemo)

A Quasar Project

## Install the dependencies
```bash
yarn
# or
npm install
```

### Start the app in development mode (hot-code reloading, error reporting, etc.)
```bash
quasar dev
```


### Lint the files
```bash
yarn lint
# or
npm run lint
```


### Format the files
```bash
yarn format
# or
npm run format
```



### Build the app for production
```bash
quasar build
```

### Customize the configuration
See [Configuring quasar.config.js](https://v2.quasar.dev/quasar-cli-vite/quasar-config-js).
