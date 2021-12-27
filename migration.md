**19th Dec 2021**

Whats In My fridge:

```sql
Db:
CREATE DATABASE wimf
    WITH 
    OWNER = postgres
    ENCODING = 'UTF8'
    CONNECTION LIMIT = -1;
 
ingredient table:

CREATE TABLE public.ingredient
(
    id bigint,
    name character varying,
    is_deleted boolean,
    created_at timestamp without time zone,
    updated_at timestamp without time zone,
    PRIMARY KEY (id)
);

ALTER TABLE IF EXISTS public.ingredient
    OWNER to postgres;
  
ALTER TABLE IF EXISTS public.ingredient
    ALTER COLUMN is_deleted SET DEFAULT false;

```

```sql
CREATE TABLE public.recipe
(
    id bigint,
    instruction character varying,
    is_deleted boolean,
    created_at timestamp without time zone,
    updated_at timestamp without time zone,
    PRIMARY KEY (id)
);

ALTER TABLE IF EXISTS public.recipe
    OWNER to postgres;
    
ALTER TABLE IF EXISTS public.recipe
    ALTER COLUMN is_deleted SET DEFAULT false;
    
    
ALTER TABLE IF EXISTS public.recipe
    ADD COLUMN name character varying;
    
```
    
```sql

CREATE TABLE public.ingredient_has_recipe
(
    ingredient_id bigint NOT NULL,
    recipe_id bigint NOT NULL,
    PRIMARY KEY (ingredient_id, recipe_id),
    CONSTRAINT fk_ingredient_has_recipe_ingredient1 FOREIGN KEY (ingredient_id)
        REFERENCES public.ingredient (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
        NOT VALID,
    CONSTRAINT fk_ingredient_has_recipe_recipe1 FOREIGN KEY (recipe_id)
        REFERENCES public.recipe (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
        NOT VALID
);

ALTER TABLE IF EXISTS public.ingredient_has_recipe
    OWNER to postgres;

```

