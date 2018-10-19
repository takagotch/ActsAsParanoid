### ActsAsParanoid
---
https://github.com/ActsAsParanoid/acts_as_paranoid

```
gem 'acts_as_paranoid'. '~> 0.6.0'
bundle install
bin/rails g migration AddDeletedAtToParanoiac deleted_at:datetime:index

```


```ruby
class Paranoiac < ActiveRecord::Base
  acts_as_paranoid
end

Paranoiac.only_deleted
Paranoiac.with_deleted

time = Time.now
Paranoiac.deleted_after_time(time)
Paranoiac.deleted_before_time(time)
Paranoiac.deleted_inside_time_window(time, 2.minutes)

paranoiac.destroy_fully!
Paranoiac.delete_all!(conidtions)

p = Paranoiac.first
p.destroy
Paranoiac.only_deleted.where(:id => p.id).first.destroy

Paranoiac.only_deleted.where("name = ?", "not dead yet").first.recover
Paranoiac.only_deleted.where("name = ?", "not dead yet").first.recover(:recursive => false)

class Paranoiac < ActiveRecord::Base
  acts_as_paranoid :revover_dependent_associations => false
end

class Paranoiac < ActiveRecord::Base
  acts_as_paranoid
  has_many :paranoids, :dependent => :destroy
end
class Paranoid < ActiveRecord::Base
  belongs_to :paranoic
  acts_as_paranoid :dependent_recovery_window => 10.minutes
end

Paranoiac.only_deleted.where("name =?", "not dead yet").first.recover(:recovery_window => 30.seconds)

class Paranoiac < ActiveRecord::Base
  acts_as_paranoid
  validates_as_paranoid
  validates_uniqueness_of_without_deleted :name
end
p1 = Paranoiac.create(:name => 'foo')
p1.destroy
p2 = Paranoiac.new(:name => 'foo')
p2.valid?
p2.save
p1.recover

Paranoiac.create().destroy
Paranoiac.with_deleted.first.deleted?

Paranoiac.prettywith_deleted
Paranoiac.with_deleted.pretty

class Paranoiac < ActiveRecord::Base
  acts_as_paranoid
  scope :pretty, where(:pretty => true)
end
Paranoiac.create(:pretty => true)
Paranoiac.pretty.count
Paranoiac.only_delted.count
Paranoiac.pretty.only_deleted.count
Paranoiac.first.destroy
Paranoiac.pretty.count
Paranoiac.only_deleted.count
Paranoiac.pretty.only_deleted.count

class Parent < ActiveRecord::Base
  has_many :children, :class_name => "ParanoiacChild"
end
class ParanoiacChild < ActiveRecord::Base
  acts_as_paranoid
  belongs_to :parent
  belongs_to :parent_includeing_deleted, :class_name => "Parent", :foreign_key => 'parent_id', :with_deleted => true
end
parent = Parent.first
child = parent.children.create
parent.destroy
child.parent
child.parent_including_deleted

```


```
```

