<template>
    <nav :class="[`navbar-${theme}`, `bg-${theme}`, 'navbar', 'navbar-expand-lg']">
        <div class="container-fluid">
            <a
                href="#"
                class="navbar-brand"
            >My Vue</a>
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">

                <navbar-link
                    v-for="(page, index) in publishedPages"
                    class="nav-item"
                    :key="index"
                    :page="page"
                    :index="index"
                    :isActive="activePage === index"
                ></navbar-link>

                <li>
                    <router-link
                        to="/create"
                        class="nav-link"
                        aria-current="page"
                    >Create Page</router-link>
                </li>
            </ul>
            <form class="d-flex">
                <button
                    class="btn btn-primary"
                    @click.prevent="changeTheme()"
                >
                    Toggle navbar
                </button>
            </form>
        </div>
    </nav>
</template>

<script>
import NavbarLink from "./NavbarLink.vue"

export default {
    components: { NavbarLink },
    created() {
        this.getThemeSetting()
    },
    computed: {
        publishedPages() {
            return this.pages.filter(p => p.published)
        }
    },
    props: ["pages", "activePage"],
    data() {
        return {
            theme: "light",
        };
    },
    methods: {
        changeTheme() {
            if (this.theme == "light") {
                this.theme = "dark";

                return;
            }

            this.theme = "light";
            this.storeThemeSetting()
        },
        storeThemeSetting() {
            localStorage.setItem("theme", this.theme)
        },
        getThemeSetting() {
            let theme = localStorage.getItem("theme")

            if (theme) {
                this.theme = theme
            }
        }
    },
}
</script>