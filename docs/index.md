---
title: KAMIKAZE
---

<div class="kz">
  <div class="kz-top">JEE Advanced college predictor · discussion forum · counselling links</div>
  <ul class="kz-menu">
    <li><a href="#forum">Forum</a></li>
    <li class="active"><a href="#predictor">Predictor</a></li>
    <li><a href="#links">Links</a></li>
    <li><a href="#run-it-locally">Run it</a></li>
  </ul>
  <div class="kz-band">
    <h1 class="kz-title">Kamikaze</h1>
    <p>Find the institutes and branches that fit your rank, based on previous years' JoSAA cutoffs.</p>
  </div>
</div>

```
This is a project for predicting prospective universities and colleges based on previous years' cutoffs. It also provides a platform for discussion, which is still under progress. Some links are mentioned on the website for further consultancy.
```
{: .quote}

<div class="kz-cards">
  <a class="kz-card" href="#predictor"><strong>Predictor</strong><span>Enter your rank, category and seat pool to see every institute and branch whose opening to closing rank range includes it.</span></a>
  <a class="kz-card" href="#forum"><strong>Forum</strong><span>Start a topic about colleges or counselling and let others reply under it.</span></a>
  <a class="kz-card" href="#links"><strong>Links</strong><span>JoSAA and other counselling resources in one place.</span></a>
</div>

---

## Predictor

###### 1 `A seat is a row of previous years' cutoffs: institute, branch, quota, category, seat pool, opening rank, closing rank`

<ul class="kz-fields">
  <li>institute_name</li><li>branch_name</li><li>allotted_quota</li><li>category</li><li>seat_pool</li><li>opening_rank</li><li>closing_rank</li>
</ul>

###### 2 `Your rank fits a seat when opening_rank ≤ rank ≤ closing_rank`

The predictor page filters every row by **category** and **seat pool**, then keeps the seats whose
opening rank is at most your rank and whose closing rank is at least your rank. It's built with
`django-filter`, and the results are sorted by institute name.

- [**`jeeadvpred/models.py`**][rank-model]
- [**`jeeadvpred/filters.py`**][rank-filter]

---

## Forum

###### 3 `Forums hold topics, and each topic holds its own discussion`

<ul class="kz-fields">
  <li>name</li><li>email</li><li>topic</li><li>description</li><li>link</li><li>date_created</li>
</ul>

The home page lists the active forums and their count. **Add more** opens a form for a new topic,
and replies are saved as `Discussion` rows that belong to that topic.

- [**`discussion_forum/models.py`**][forum-model]
- [**`discussion_forum/views.py`**][forum-views]

---

## Links

###### 4 `Useful info for counselling, linked from the site`

<ul class="kz-links">
  <li><a href="https://josaa.nic.in/" target="_blank" rel="noopener noreferrer">JoSAA</a></li>
  <li><a href="https://www.facebook.com/groups/3464210553673965/?ref=share" target="_blank" rel="noopener noreferrer">Official JEE counselling group on Facebook</a></li>
</ul>

---

## Run it locally

###### 5 `Django 3.1 · django-filter · MySQL`

Kamikaze needs Python 3.9 or older, because Django 3.1 doesn't run on newer versions. It reads its
MySQL connection from `/etc/mysql/my.cnf`.

```
git clone https://github.com/repsick3r/kamikaze.git
cd kamikaze
python3.9 -m venv .venv && source .venv/bin/activate
pip install "django>=3.1,<3.2" "django-filter<2.5" mysqlclient
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver 8000
```

Keep the port at `8000`, because the menu links in the templates point to `http://127.0.0.1:8000/`.
The predictor starts with no data, so add cutoff rows through **Admin** at `/admin/`.

```
kamikaze/
├── kamikaze/           settings, urls, templates (home, links, base) and static CSS
├── jeeadvpred/         the rank model, its filter and the predictor page
├── discussion_forum/   forum and discussion models, and the forms to add them
└── manage.py
```

---

<p class="kz-credit">Built by Repala Sudhamsh and Mohit Lunia · <a href="https://github.com/repsick3r/kamikaze">Code on GitHub</a></p>

[rank-model]: https://github.com/repsick3r/kamikaze/blob/master/jeeadvpred/models.py
[rank-filter]: https://github.com/repsick3r/kamikaze/blob/master/jeeadvpred/filters.py
[forum-model]: https://github.com/repsick3r/kamikaze/blob/master/discussion_forum/models.py
[forum-views]: https://github.com/repsick3r/kamikaze/blob/master/discussion_forum/views.py
