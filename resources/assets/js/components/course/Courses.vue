<template>
    <div class="container">
        <div class="row py-3">
            <div class="col">
                <h3>Courses</h3>
            </div>
            <div class="col">
                <div class="row">
                    <div class="col">
                        <div class="dropdown">
                            <a
                                id="dropdownMenuLink"
                                class="btn btn-secondary dropdown-toggle"
                                href="#"
                                role="button"
                                data-toggle="dropdown"
                                aria-haspopup="true"
                                aria-expanded="false"
                            >
                                Sort By
                            </a>

                            <div
                                class="dropdown-menu"
                                aria-labelledby="dropdownMenuLink"
                            >
                                <a
                                    class="dropdown-item"
                                    href="javascript:void(0)"
                                ><span>Recently Accessed</span></a>
                                <a
                                    class="dropdown-item"
                                    href="javascript:void(0)"
                                ><span>Recently Enrolled</span></a>
                                <a
                                    class="dropdown-item"
                                    href="javascript:void(0)"
                                ><span>Title: A-to-Z</span></a>
                                <a
                                    class="dropdown-item"
                                    href="javascript:void(0)"
                                ><span>Title: Z-to-A</span></a>
                                <a
                                    class="dropdown-item"
                                    href="javascript:void(0)"
                                ><span>Completion: 0% to 100%</span></a>
                                <a
                                    class="dropdown-item"
                                    href="javascript:void(0)"
                                ><span>Completion: 100% to 0%</span></a>
                            </div>
                        </div>
                    </div>
                    <div class="col">
                        <form
                            class=""
                            _lpchecked="1"
                        >
                            <label
                                for="search-courses-input"
                                class="control-label sr-only"
                            >Search my courses</label><span class="input-group"><input
                                id="search-courses-input"
                                placeholder="Search my courses"
                                required=""
                                autocomplete="off"
                                class="form-control"
                                value=""
                            ><span class="input-group-btn"><button
                                aria-label="Search my courses"
                                type="submit"
                                class="btn btn-secondary"
                                disabled=""
                            ><span class="fas fa-search" /></button>
                            </span>
                            </span>
                        </form>
                    </div>
                    <div class="col">
                        <a
                            href=""
                            class="btn btn-primary"
                            @click.prevent="create = !create"
                        >Create Course</a>
                    </div>
                </div>
            </div>
        </div>
        <div
            v-if="create"
            class="row"
        >
            <div class="col">
                <NewCourse />
            </div>
        </div>
        <div class="row course-list">
            <div
                v-for="course in courses"
                :key="course.id"
                class="col col-3"
            >
                <Course
                    :course="course"
                    class="is-link"
                    buttonable
                    button="Start Edit"
                    @click.native.prevent="linkToSingle(course)"
                />
            </div>
        </div>
    </div>
</template>

<script>
import NewCourse from './NewCourse'
import Course from '@c/common/Course'
export default {
    components: {
        NewCourse,
        Course
    },
    data () {
        return {
            create: false,
            courses: []
        }
    },
    computed: {

    },
    created () {
        this.getCourses()
    },
    methods: {
        getCourses () {
            axios.get('/api/course')
                .then(res => {
                    this.courses = res.data.data
                })
        },
        linkToSingle (course) {
            this.$router.push({
                name: 'course-single',
                params: {
                    id: course.id
                }
            })
        }
    }
}
</script>
