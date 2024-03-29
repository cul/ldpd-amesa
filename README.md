# ldpd-amesa

## First-Time Setup (for developers)

- Install ruby
- Install NodeJS (tested with versions 8 and 10)
- Install yarn

### And then:

```
git clone git@github.com:cul/ldpd-amesa.git # Clone the repo
cd ldpd-amesa # Switch to the application directory

# Note: Assuming you're using RVM, RVM should automatically selected the correct ruby version when you cd into the project directory.  In this case, it'sspecified in Gemfile, which RVM is aware of in recent versions.  Verify that the correct version has been selected.

bundle install # Install ruby gem dependencies
yarn install # Install node module depencencies
bundle exec rake amesa:setup:config_files # Set up required config files
rails db:migrate RAILS_ENV=development # Run database migrations

# Start the application using the rails server command
rails s -p 3000
```

## PHP Notes
### Controllers
* Controller
    * AppController
        * AdminController
        * CountriesController
        * EmailAddressesController
        * LanguagesController
        * PagesController
        * PendingScholarEditsController
        * PendingScholarsController
        * RegionsController
        * ScholarsController
        * TextBlocksController

### Entities
* Model
    * AppModel
        * Country
            * attributes
                * id: not blank, numeric, 1..10000
                * name: not blank, varchar(255)
                * fra_name: not blank, varchar(255)
            * has many: ScholarEdit, Scholar
        * EmailAddress
            * attributes
                * name: not blank
        * Language
            * attributes
                * name: not blank; dup maxLength keys indicate validation problem
                * three_letter_code: not blank; dup maxLength keys indicate validation problem
        * Region
            * attributes
                * name: not blank, varchar(100)
                * fra_name: not blank, varchar(100)
                * url_formatted_name: not blank, varchar(4:30)
            * has many: ScholarEdit, Scholar
        * Scholar
            * attributes
                * region_id
                * country_id
                * name_part_1: not blank, varchar(100)
                * name_part_2: not blank, varchar(100)
                * title: varchar(100)
                * affiliation: varchar(300)
                * mailing_address
                * phone_fax_numbers
                * websites
                * education
                * research
                * teaching
                * email
                * submitter_email
                * countries_of_specialization
                * publications
                * keywords
                * optional_message
                * warning
                * status
            * belongs to: Region, Country
            * has many: ScholarEdit
        * ScholarEdit
            * attributes: from Scholar
            * belongs to: Scholar, Region, Country
        * TextBlock
            * attributes
                * home_page_title_1: not blank
                * home_page_col_1: not blank
                * home_page_title_2: not blank
                * home_page_col_2: not blank
                * home_page_title_3: not blank
                * home_page_col_3: not blank
                * home_page_title_4: not blank
                * home_page_col_4: not blank
                * about_page_title: not blank
                * about_page: not blank

