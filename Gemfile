source 'https://rubygems.org'

gemspec

# We need a newish Rake since Active Job sets its test tasks' descriptions.
gem 'rake', '>= 11.1'

# This needs to be with require false to ensure correct loading order, as it has to
# be loaded after loading the test library.
gem 'mocha', '~> 0.14', require: false

gem 'rack-cache', '~> 1.5', '>= 1.5.1'
gem 'jquery-rails', '>= 4.1.1'
gem 'coffee-rails', '~> 4.2.2'
gem 'turbolinks', github: 'turbolinks/turbolinks-rails'

# require: false so bcrypt is loaded only when has_secure_password is used.
# This is to avoid Active Model (and by extension the entire framework)
# being dependent on a binary library.
gem 'bcrypt', '~> 3.1.11', require: false

# This needs to be with require false to avoid it being automatically loaded by
# sprockets.
gem 'uglifier', '>= 1.3.0', require: false

# Track stable branch of sass because it doesn't have circular require warnings.
gem 'sass', github: 'sass/sass', branch: 'stable', require: false

group :doc do
  gem 'sdoc', '~> 0.4.0'
  gem 'redcarpet', '~> 3.2.3', platforms: :ruby
  gem 'w3c_validators'
  gem 'kindlerb', '0.1.1'
end

# Active Support.
gem 'dalli', '>= 2.2.1'
gem 'listen', '~> 3.0.5', require: false

# Active Job.
group :job do
  gem 'resque', '>= 1.25.2', '< 1.26', require: false
  gem 'resque-scheduler', require: false
  gem 'sidekiq', require: false
  gem 'sucker_punch', require: false
  gem 'delayed_job', '>= 4.1.9', require: false
  gem 'queue_classic', github: "QueueClassic/queue_classic", branch: 'master', require: false, platforms: :ruby
  gem 'sneakers', require: false
  gem 'que', require: false
  gem 'backburner', require: false
  gem 'qu-rails', github: "bkeepers/qu", branch: "master", require: false
  gem 'qu-redis', require: false
  gem 'delayed_job_active_record', '>= 4.1.5', require: false
  gem 'sequel', require: false
end

# Action Cable
group :cable do
  gem 'puma', require: false

  gem 'em-hiredis', require: false
  gem 'hiredis', require: false
  gem 'redis', require: false

  gem 'faye-websocket', require: false
end

# Add your own local bundler stuff.
local_gemfile = File.dirname(__FILE__) + "/.Gemfile"
instance_eval File.read local_gemfile if File.exist? local_gemfile

group :test do
  # FIX: Our test suite isn't ready to run in random order yet.
  gem 'minitest', '< 5.3.4'

  platforms :mri do
    gem 'stackprof'
    gem 'byebug'
  end

  gem 'benchmark-ips'
end

platforms :ruby, :mswin, :mswin64, :mingw, :x64_mingw do
  gem 'nokogiri', '>= 1.6.7.1'

  # Needed for compiling the ActionDispatch::Journey parser.
  gem 'racc', '>=1.4.6', require: false

  # Active Record.
  gem 'sqlite3', '~> 1.3.6'

  group :db do
    gem 'pg', '>= 0.18.0'
    gem 'mysql2', '>= 0.4.0'
  end
end

platforms :jruby do
  if ENV['AR_JDBC']
    gem 'activerecord-jdbcsqlite3-adapter', github: 'jruby/activerecord-jdbc-adapter', branch: 'master'
    group :db do
      gem 'activerecord-jdbcmysql-adapter', github: 'jruby/activerecord-jdbc-adapter', branch: 'master'
      gem 'activerecord-jdbcpostgresql-adapter', github: 'jruby/activerecord-jdbc-adapter', branch: 'master'
    end
  else
    gem 'activerecord-jdbcsqlite3-adapter', '>= 1.3.0'
    group :db do
      gem 'activerecord-jdbcmysql-adapter', '>= 1.3.0'
      gem 'activerecord-jdbcpostgresql-adapter', '>= 1.3.0'
    end
  end
end

platforms :rbx do
  # The rubysl-yaml gem doesn't ship with Psych by default as it needs
  # libyaml that isn't always available.
  gem 'psych', '~> 2.0'
end

# Gems that are necessary for Active Record tests with Oracle.
if ENV['ORACLE_ENHANCED']
  platforms :ruby do
    gem 'ruby-oci8', '~> 2.2'
  end
  gem 'activerecord-oracle_enhanced-adapter', github: 'rsim/oracle-enhanced', branch: 'master'
end

# A gem necessary for Active Record tests with IBM DB.
gem 'ibm_db' if ENV['IBM_DB']
gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]
