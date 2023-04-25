from django.shortcuts import get_object_or_404, render
from blog.models import Post, Category
from django.db.models import Q
from datetime import datetime
import pytz

def index(request):
    template = 'blog/index.html'
    post_list = Post.objects.all(
        ).filter(
            is_published=True,
            category__is_published=True,
            pub_date__lte = datetime.now(tz=pytz.UTC)
            )[:5]
    context = {'post_list':post_list}
    return render(request, template, context)


def post_detail(request, post_id):
    template = 'blog/detail.html'
    post = get_object_or_404(Post.objects.filter(
        Q(is_published = True) 
        & Q(category__is_published = True) 
        & Q(pub_date__lte = datetime.now(tz=pytz.UTC))
        ), pk=post_id)
    context = {'post': post}
    return render(request, template, context)

#found_posts = [x for x in Post.objects.get(post_id=post_id) if x["id"] == int(post_id)]
    #context = {'post': found_posts[0]} if len(found_posts) > 0 else None


def category_posts(request, category_slug):
    template = 'blog/category.html'
    category = get_object_or_404(Category.objects.values('title', 'description').filter(slug=category_slug, is_published = True))
    post_list = Post.objects.filter(
            category__slug=category_slug,
            is_published = True,
            category__is_published=True,
            pub_date__lte = datetime.now(tz=pytz.UTC)
            )
    context = {'category': category, 'post_list':post_list}
    return render(request, template, context)
