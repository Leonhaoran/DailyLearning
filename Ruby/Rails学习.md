### Rails console
假设我们有两个模型(Models)，Recipe和Category。

    Recipe
        title :string
        belongs_to :Category
    
    Category
        name :string
        has_many :Recipe

    如果想查看Model的所有实例：
        Recipe.all
        Category.all

    如果想修改某个Recipe实例的title：
        需要知道该Recipe实例的id
        recipe_to_update=Recipe.find(recipe_id)
        recipe_to_update.title='new_title'
        recipe_to_update.save

### ERB(Embedded Ruby)      
<%  %>括起来的是Ruby代码