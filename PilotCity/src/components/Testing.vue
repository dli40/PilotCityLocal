<template>
    <div>
        <build />
    </div>
</template>
<script>
import w_skills from '@/components/wizard/teacher/w_skills'
import w_teacher_address from '@/components/wizard/teacher/w_teacher_address'
import w_industry from '@/components/wizard/teacher/w_industry'
import w_story from '@/components/wizard/teacher/w_story'
import w_class from '@/components/wizard/teacher/w_class'
import w_tymod from '@/components/wizard/teacher/w_tymod'
import w_address from '@/components/wizard/employer/w_address'
import w_sector from '@/components/wizard/employer/w_sector'
import w_bottom_line from '@/components/wizard/employer/w_bottom_line'
import w_solutions_tagging from '@/components/wizard/employer/w_solutions_tagging'
import w_tags from '@/components/wizard/employer/w_tags'
import w_solutions_picker from '@/components/wizard/employer/w_solutions_picker'
import w_department from '@/components/wizard/employer/w_department'
import w_employer_story from '@/components/wizard/employer/w_employer_story'
import w_flock from '@/components/wizard/employer/w_flock'
import w_ptype from '@/components/wizard/teacher/w_ptype'
import w_curriculum from '@/components/wizard/teacher/w_curriculum'
import Matchmade from '@/components/Matchmade'
import w_tymod_employer from '@/components/wizard/employer/w_tymod_employer'
import Foremployer from '@/components/Foremployer'
import Forteacher from '@/components/Forteacher'
import Backgroundvideo from '@/components/Backgroundvideo'
import employer from '@/components/dashboard/employer'
import challenge from '@/components/builder/challenge'
import build from '@/components/builder/build'
import experience from '@/components/builder/experience'

export default {
    name: 'Testing',
    data (){
        return {
            
        }
    },
    components:
    {
        w_skills,
        w_teacher_address,
        w_industry,
        w_story,
        w_class,
        w_tymod,
        w_address,
        w_sector,
        w_bottom_line,
        w_solutions_tagging,
        w_flock,
        w_tags,
        w_solutions_picker,
        w_department,
        w_employer_story,
        w_ptype,
        w_curriculum,
        Matchmade,
        w_tymod_employer,
        Foremployer,
        Forteacher,
        Backgroundvideo,
        employer,
        challenge,
        build,
        experience,


    }
}
</script>
