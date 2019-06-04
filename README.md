# README

You need Language change setting . Follow me

##* Step 1 - gem 'rails-i18n'

* Step 2 - config/application.rb
         -- config.i18n.available_locales = [:en, :ru]
            config.i18n.default_locale = :en

* Step 3 - create config/locales ru.yml
         -- ru:
                welcome: "Добро пожаловать!"

* Step 4 - routes.rb
         -- scope "(:locale)", locale: /#{I18n.available_locales.join("|")}/ do
                # your routes here...
            end

* Step 5 - application_controller.rb
         -- before_action :set_locale
            private
                def set_locale
                I18n.locale = extract_locale || I18n.default_locale
                end
            def extract_locale
                parsed_locale = params[:locale]
                I18n.available_locales.map(&:to_s).include?(parsed_locale) ? parsed_locale : nil
            end

            def default_url_options
                { locale: I18n.locale }
            end

* Step 6 - change Language
         -- <ul>
                <li><%= link_to 'English', root_path(locale: :en) %></li>
                <li><%= link_to 'Русский', root_path(locale: :ru) %></li>
            </ul>

