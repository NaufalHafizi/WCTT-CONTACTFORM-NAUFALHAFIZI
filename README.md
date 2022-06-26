# Naufal Hafizi

## Getting Started

1. This repo contains Backend and Frontend code.
2. Make sure to setup both code to run the project properly.

## Setup Backend (Yii2)

1. Clone to your local - git clone https://github.com/NaufalHafizi/WCTT-CONTACTFORM-NAUFALHAFIZI.git
2. Open in your code editor. Setup your database instance in backend->config->db.php
3. Run these commands

```
cd backend
composer install
```

4. run the migration and select yes

```
php yii migrate
```

5. Run your local. Make sure to use port 8080. Otherwise, you need to change the port in frontend

```
php yii serve -p 8080
```

## Setup Frontend (Svelte JS & Tailwind CSS)

1. Run these commands

```
cd frontend
npm install
```

2. run your local

```
npm run dev
```

3. If you're using different port in backend localhost, change the url inside frontend->src->App.svelte
4. Since we are using the localhost, Please disable the Cors checking.

## Contributions

By [Naufal Hafizi](https://naufalhafizi.com/) 2022
